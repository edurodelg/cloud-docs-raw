---
merged_at: 2026-01-25T21:47:44.402564
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicevertexragdataservi_e80a07.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicevertexragdataservic_68b929.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicevertexragdataserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient -->

# Class VertexRagDataServiceClient (1.134.0)

```
VertexRagDataServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing user data for RAG.

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
`VertexRagDataServiceTransport` |
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

### VertexRagDataServiceClient

```
VertexRagDataServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag data service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagDataServiceTransport,Callable[..., VertexRagDataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagDataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_rag_corpus

```
create_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.CreateRagCorpusRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
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


Creates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusRequest.html)(
parent="parent_value",
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[create_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_create_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.CreateRagCorpus. |
`parent` |
`str`
Required. The resource name of the Location to create the RagCorpus in. Format: |
`rag_corpus` |
Required. The RagCorpus to create. This corresponds to the |
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

### delete_rag_corpus

```
delete_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagCorpusRequest,
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


Deletes a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagCorpusRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_delete_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagCorpus. |
`name` |
`str`
Required. The name of the RagCorpus resource to be deleted. Format: |
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

### delete_rag_file

```
delete_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.DeleteRagFileRequest,
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


Deletes a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagFileRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_delete_rag_file)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagFile. |
`name` |
`str`
Required. The name of the RagFile resource to be deleted. Format: |
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
`VertexRagDataServiceClient` |
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
`VertexRagDataServiceClient` |
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
`VertexRagDataServiceClient` |
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

### get_rag_corpus

```
get_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagCorpusRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
```


Gets a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagCorpusRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_get_rag_corpus)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagDataService.GetRagCorpus |
`name` |
`str`
Required. The name of the RagCorpus resource. Format: |
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
A RagCorpus is a RagFile container and a project can have multiple RagCorpora. |

### get_rag_engine_config

```
get_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagEngineConfigRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
```


Gets a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagEngineConfigRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_get_rag_engine_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagDataService.GetRagEngineConfig |
`name` |
`str`
Required. The name of the RagEngineConfig resource. Format: |
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
Config for RagEngine. |

### get_rag_file

```
get_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.GetRagFileRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
```


Gets a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagFileRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_get_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagDataService.GetRagFile |
`name` |
`str`
Required. The name of the RagFile resource. Format: |
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
A RagFile contains user data for chunking, embedding and indexing. |

### import_rag_files

```
import_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ImportRagFilesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
import_rag_files_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.ImportRagFilesConfig
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


Import files from Google Cloud Storage or Google Drive into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_import_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
import_rag_files_config = aiplatform_v1beta1.[ImportRagFilesConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesConfig.html)()
import_rag_files_config.gcs_source.uris = ['uris_value1', 'uris_value2']
import_rag_files_config.partial_failure_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
import_rag_files_config.import_result_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ImportRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesRequest.html)(
parent="parent_value",
import_rag_files_config=import_rag_files_config,
)
# Make the request
operation = client.[import_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_import_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ImportRagFiles. |
`parent` |
`str`
Required. The name of the RagCorpus resource into which to import files. Format: |
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. This corresponds to the |
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

### list_rag_corpora

```
list_rag_corpora(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaPager
)
```


Lists RagCorpora in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_rag_corpora():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagCorporaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_corpora](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_list_rag_corpora)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagCorpora. |
`parent` |
`str`
Required. The resource name of the Location from which to list the RagCorpora. Format: |
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
Response message for VertexRagDataService.ListRagCorpora. Iterating over this object will yield results and resolve additional pages automatically. |

### list_rag_files

```
list_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesPager
)
```


Lists RagFiles in a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_rag_files():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_list_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagFiles. |
`parent` |
`str`
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: |
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
Response message for VertexRagDataService.ListRagFiles. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_rag_engine_config_path

`parse_rag_engine_config_path(path: str) -> typing.Dict[str, str]`


Parses a rag_engine_config path into its component segments.

### parse_rag_file_path

`parse_rag_file_path(path: str) -> typing.Dict[str, str]`


Parses a rag_file path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### rag_engine_config_path

`rag_engine_config_path(project: str, location: str) -> str`


Returns a fully-qualified rag_engine_config string.

### rag_file_path

`rag_file_path(project: str, location: str, rag_corpus: str, rag_file: str) -> str`


Returns a fully-qualified rag_file string.

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

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

### update_rag_corpus

```
update_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagCorpusRequest,
dict,
]
] = None,
*,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagCorpus
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


Updates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_rag_corpus():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1beta1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagCorpusRequest.html)(
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[update_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_update_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagCorpus. |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. This corresponds to the |
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

### update_rag_engine_config

```
update_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UpdateRagEngineConfigRequest,
dict,
]
] = None,
*,
rag_engine_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagEngineConfig
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


Updates a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_rag_engine_config():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest.html)(
)
# Make the request
operation = client.[update_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_update_rag_engine_config)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagEngineConfig. |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. This corresponds to the |
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

### upload_rag_file

```
upload_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_file: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.RagFile
] = None,
upload_rag_file_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data.UploadRagFileConfig
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
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.UploadRagFileResponse
)
```


Upload a file into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_upload_rag_file():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagDataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html)()
# Initialize request argument(s)
rag_file = aiplatform_v1beta1.[RagFile](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile.html)()
rag_file.gcs_source.uris = ['uris_value1', 'uris_value2']
rag_file.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileRequest.html)(
parent="parent_value",
rag_file=rag_file,
)
# Make the request
response = client.[upload_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_data_service_VertexRagDataServiceClient_upload_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for VertexRagDataService.UploadRagFile. |
`parent` |
`str`
Required. The name of the RagCorpus resource into which to upload the file. Format: |
`rag_file` |
Required. The RagFile to upload. This corresponds to the |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. This corresponds to the |
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
Response message for VertexRagDataService.UploadRagFile. |

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesragfileparsingconfigllmparser_googlecloud_29688f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesragfileparsingconfigllmparser_googleclouda_5b6928.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesragfileparsingconfigllmparser_googlecloudai_89fcba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragfileparsingconfigllmparser_googlecloudaip_5d783b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragfileparsingconfigllmparser_googlecloudaipl_b5330c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfileparsingconfigllmparser.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig.LlmParser -->

# Class LlmParser (1.134.0)

`LlmParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the LLM parsing for RagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`model_name` |
`str`
The name of a LLM model used for parsing. Format: - `projects/{project_id}/locations/{location}/publishers/{publisher}/models/{model}`
|
`max_parsing_requests_per_min` |
`int`
The maximum number of requests the job is allowed to make to the LLM model per minute. Consult https://cloud.google.com/vertex-ai/generative-ai/docs/quotas and your document size to set an appropriate value here. If unspecified, a default value of 5000 QPM would be used. |
`global_max_parsing_requests_per_min` |
`int`
The maximum number of requests the job is allowed to make to the LLM model per minute in this project. Consult https://cloud.google.com/vertex-ai/generative-ai/docs/quotas and your document size to set an appropriate value here. If this value is not specified, max_parsing_requests_per_min will be used by indexing pipeline job as the global limit. |
`custom_parsing_prompt` |
`str`
The prompt to use for parsing. If not specified, a default prompt will be used. |

## Methods

### LlmParser

`LlmParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the LLM parsing for RagFiles.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeswritefeaturevaluespayload.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesPayload -->

# Class WriteFeatureValuesPayload (1.134.0)

`WriteFeatureValuesPayload(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains Feature values to be written for a specific entity.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
Required. The ID of the entity. |
`feature_values` |
`MutableMapping[str, `
Required. Feature values to be written, mapping from Feature ID to value. Up to 100,000 `feature_values` entries may be
written across all payloads. The feature generation time,
aligned by days, must be no older than five years (1825
days) and no later than one year (366 days) in the future.
|

## Classes

### FeatureValuesEntry

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### WriteFeatureValuesPayload

`WriteFeatureValuesPayload(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains Feature values to be written for a specific entity.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfig__googleclou_d7f466.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig -->

# Class ConnectorConfig (1.134.0)

`ConnectorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for importing data from an external source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`big_query_source_config` |
Configuration for importing data from a BigQuery table. This field is a member of `oneof` _ `source` .
|

## Classes

### BigQuerySourceConfig

`BigQuerySourceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for importing data from a BigQuery table.

### DatapointFieldMapping

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.

## Methods

### ConnectorConfig

`ConnectorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for importing data from an external source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstopnotebookruntimeresponse_googlecloudaiplatform__454a09.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstopnotebookruntimeresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopNotebookRuntimeResponse -->

# Class StopNotebookRuntimeResponse (1.134.0)

`StopNotebookRuntimeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for NotebookService.StopNotebookRuntime.

## Methods

### StopNotebookRuntimeResponse

`StopNotebookRuntimeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for NotebookService.StopNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescoherencespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceSpec -->

# Class CoherenceSpec (1.134.0)

`CoherenceSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence score metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### CoherenceSpec

`CoherenceSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence score metric.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesprivateserviceconnectconfig_googlecloudaipla_467fbc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesprivateserviceconnectconfig_googlecloudaiplat_167ff9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprivateserviceconnectconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrivateServiceConnectConfig -->

# Class PrivateServiceConnectConfig (1.134.0)

`PrivateServiceConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents configuration for private service connect.

## Attributes |
|
|---|---|
Name |
Description |
`enable_private_service_connect` |
`bool`
Required. If true, expose the IndexEndpoint via private service connect. |
`project_allowlist` |
`MutableSequence[str]`
A list of Projects from which the forwarding rule will target the service attachment. |
`psc_automation_configs` |
`MutableSequence[`
Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only. |
`enable_secure_private_service_connect` |
`bool`
Optional. If set to true, enable secure private service connect with IAM authorization. Otherwise, private service connect will be done without authorization. Note latency will be slightly increased if authorization is enabled. |
`service_attachment` |
`str`
Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect. |

## Methods

### PrivateServiceConnectConfig

`PrivateServiceConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents configuration for private service connect.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecparameterspecdoublevaluespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.DoubleValueSpec -->

# Class DoubleValueSpec (1.134.0)

`DoubleValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DOUBLE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`min_value` |
`float`
Required. Inclusive minimum value of the parameter. |
`max_value` |
`float`
Required. Inclusive maximum value of the parameter. |
`default_value` |
`float`
A default value for a `DOUBLE` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### DoubleValueSpec

`DoubleValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DOUBLE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespart.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Part -->

# Class Part (1.134.0)

`Part(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

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
`text` |
`str`
Optional. Text part (can be code). This field is a member of `oneof` _ `data` .
|
`inline_data` |
Optional. Inlined bytes data. This field is a member of `oneof` _ `data` .
|
`file_data` |
Optional. URI based data. This field is a member of `oneof` _ `data` .
|
`function_call` |
Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values. This field is a member of `oneof` _ `data` .
|
`function_response` |
Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model. This field is a member of `oneof` _ `data` .
|
`executable_code` |
Optional. Code generated by the model that is meant to be executed. This field is a member of `oneof` _ `data` .
|
`code_execution_result` |
Optional. Result of executing the [ExecutableCode]. This field is a member of `oneof` _ `data` .
|
`video_metadata` |
Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data. This field is a member of `oneof` _ `metadata` .
|
`thought` |
`bool`
Indicates if the part is thought from the model. |
`thought_signature` |
`bytes`
An opaque signature for the thought so it can be reused in subsequent requests. |

## Methods

### Part

`Part(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformtensorboardexperiment__googlecloudaiplatform_v1servicesjob_20ca70.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformtensorboardexperiment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardExperiment -->

# Class TensorboardExperiment (1.134.0)

```
TensorboardExperiment(
tensorboard_experiment_name: str,
tensorboard_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed tensorboard resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

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

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### TensorboardExperiment

```
TensorboardExperiment(
tensorboard_experiment_name: str,
tensorboard_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing tensorboard experiment given a tensorboard experiment name or ID.

Example Usage:

```
tb_exp = aiplatform.TensorboardExperiment(
tensorboard_experiment_name= "projects/123/locations/us-central1/tensorboards/456/experiments/678"
)
tb_exp = aiplatform.TensorboardExperiment(
tensorboard_experiment_name= "678"
tensorboard_id = "456"
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_name` |
`str`
Required. A fully-qualified tensorboard experiment resource name or resource ID. Example: "projects/123/locations/us-central1/tensorboards/456/experiments/678" or "678" when tensorboard_id is passed and project and location are initialized or passed. |
`tensorboard_id` |
`str`
Optional. A tensorboard resource ID. |
`project` |
`str`
Optional. Project to retrieve tensorboard from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve tensorboard from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Tensorboard. Overrides credentials set in aiplatform.init. |

### create

```
create(
tensorboard_experiment_id: str,
tensorboard_name: str,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Sequence[typing.Tuple[str, str]] = (),
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardExperiment
```


Creates a new TensorboardExperiment.

Example Usage:

```
tb_exp = aiplatform.TensorboardExperiment.create(
tensorboard_experiment_id='my-experiment'
tensorboard_id='456'
display_name='my display name',
description='my description',
labels={
'key1': 'value1',
'key2': 'value2'
}
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_id` |
`str`
Required. The ID to use for the Tensorboard experiment, which will become the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are / |
`tensorboard_name` |
`str`
Required. The resource name or ID of the Tensorboard to create the TensorboardExperiment in. Format of resource name: |
`display_name` |
`str`
Optional. The user-defined name of the Tensorboard Experiment. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. Description of this Tensorboard Experiment. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`project` |
`str`
Optional. Project to upload this model to. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to upload this model to. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`TensorboardExperiment` |
The TensorboardExperiment resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### list

```
list(
tensorboard_name: str,
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[
google.cloud.aiplatform.tensorboard.tensorboard_resource.TensorboardExperiment
]
```


List TensorboardExperiemnts in a Tensorboard resource.

```
Example Usage:
aiplatform.TensorboardExperiment.list(
tensorboard_name='projects/my-project/locations/us-central1/tensorboards/123'
)
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_name` |
`str`
Required. The resource name or resource ID of the Tensorboard to list TensorboardExperiments. Format, if resource name: 'projects/{project}/locations/{location}/tensorboards/{tensorboard}' |
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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerssearchmodeldeploymentmonitorin_353449.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerssearchmodeldeploymentmonitoringstatsanomaliespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesPager

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessummarizationverbosityinstance_googlecloudaip_37e08b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessummarizationverbosityinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityInstance -->

# Class SummarizationVerbosityInstance (1.134.0)

```
SummarizationVerbosityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to be summarized. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Optional. Summarization prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### SummarizationVerbosityInstance

```
SummarizationVerbosityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundingsupport.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingSupport -->

# Class GroundingSupport (1.134.0)

`GroundingSupport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding support.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`segment` |
Segment of the content this support belongs to. This field is a member of `oneof` _ `_segment` .
|
`grounding_chunk_indices` |
`MutableSequence[int]`
A list of indices (into 'grounding_chunk') specifying the citations associated with the claim. For instance [1,3,4] means that grounding_chunk[1], grounding_chunk[3], grounding_chunk[4] are the retrieved content attributed to the claim. |
`confidence_scores` |
`MutableSequence[float]`
Confidence score of the support references. Ranges from 0 to 1. 1 is the most confident. This list must have the same size as the grounding_chunk_indices. |

## Methods

### GroundingSupport

`GroundingSupport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding support.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesendpoint_servicepagers_googlecloudaiplatform__183eb4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesendpoint_servicepagers_googlecloudaiplatform_v_5768a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesendpoint_servicepagers_googlecloudaiplatform_v1_8f3ea0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesendpoint_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.endpoint_service.pagers`

module.

## Classes

[ListEndpointsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsAsyncPager)

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEndpointsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsPager)

```
ListEndpointsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse
],
request: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesschedule_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.schedule_service.pagers`

module.

## Classes

[ListSchedulesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesAsyncPager)

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse) object, and
provides an `__aiter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSchedulesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesPager)

```
ListSchedulesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse
],
request: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse) object, and
provides an `__iter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesragvectordbconfigpinecone_googlecloudaiplatform__f442ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesragvectordbconfigpinecone_googlecloudaiplatform_v_a707ee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragvectordbconfigpinecone_googlecloudaiplatform_v1_f5dcd8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragvectordbconfigpinecone.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.Pinecone -->

# Class Pinecone (1.134.0)

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.

## Attribute |
|
|---|---|
Name |
Description |
`index_name` |
`str`
Pinecone index name. This value cannot be changed after it's set. |

## Methods

### Pinecone

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessafetyinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyInput -->

# Class SafetyInput (1.134.0)

`SafetyInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for safety metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for safety metric. |
`instance` |
Required. Safety instance. |

## Methods

### SafetyInput

`SafetyInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for safety metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesraymetricspec_googlecloudaiplatform_v1typesfeature_8d7172.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesraymetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RayMetricSpec -->

# Class RayMetricSpec (1.134.0)

`RayMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray metrics.

## Attribute |
|
|---|---|
Name |
Description |
`disabled` |
`bool`
Optional. Flag to disable the Ray metrics collection. |

## Methods

### RayMetricSpec

`RayMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray metrics.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureselector.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureSelector -->

# Class FeatureSelector (1.134.0)

`FeatureSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for Features of an EntityType.

## Attribute |
|
|---|---|
Name |
Description |
`id_matcher` |
Required. Matches Features based on ID. |

## Methods

### FeatureSelector

`FeatureSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for Features of an EntityType.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.index_service.pagers`

module.

## Classes

[ListIndexesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesAsyncPager)

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse) object, and
provides an `__aiter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexes`

requests and continue to iterate
through the `indexes`

field on the
corresponding responses.

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListIndexesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesPager)

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse) object, and
provides an `__iter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexes`

requests and continue to iterate
through the `indexes`

field on the
corresponding responses.

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslisteventsrequest_googlecloudaiplatform_v1t_3b9d15.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslisteventsrequest_googlecloudaiplatform_v1ty_5398f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisteventsrequest_googlecloudaiplatform_v1typ_b20b0c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisteventsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest -->

# Class ListEventsRequest (1.134.0)

`ListEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.ListEvents.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the session to list events from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|
`page_size` |
`int`
Optional. The maximum number of events to return. The service may return fewer than this value. If unspecified, at most 100 events will be returned. These events are ordered by timestamp in ascending order. |
`page_token` |
`str`
Optional. The next_page_token value returned from a previous list SessionService.ListEvents call. |
`filter` |
`str`
Optional. The standard list filter. Supported fields: \* `timestamp` range (i.e.
`timestamp>="2025-01-31T11:30:00-04:00"` where the
timestamp is in RFC 3339 format)
More detail in `AIP-160 ` __.
|
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `timestamp`
Example: `timestamp desc` .
|

## Methods

### ListEventsRequest

`ListEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.ListEvents.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinefailurepolicy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineFailurePolicy -->

# Class PipelineFailurePolicy (1.134.0)

`PipelineFailurePolicy(value)`


Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.

## Enums |
|
|---|---|
Name |
Description |
`PIPELINE_FAILURE_POLICY_UNSPECIFIED` |
Default value, and follows fail slow behavior. |
`PIPELINE_FAILURE_POLICY_FAIL_SLOW` |
Indicates that the pipeline should continue to run until all possible tasks have been scheduled and completed. |
`PIPELINE_FAILURE_POLICY_FAIL_FAST` |
Indicates that the pipeline should stop scheduling new tasks after a task has failed. |

## Methods

### PipelineFailurePolicy

`PipelineFailurePolicy(value)`


Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_servicepagerslistdeploymentresourcepoolsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsAsyncPager -->

# Class ListDeploymentResourcePoolsAsyncPager (1.134.0)

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDeploymentResourcePools`

requests and continue to iterate
through the `deployment_resource_pools`

field on the
corresponding responses.

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDeploymentResourcePoolsAsyncPager

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesauthconfig__googlecloudaiplatform_v1typesstud_c0a887.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesauthconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig -->

# Class AuthConfig (1.134.0)

`AuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Auth configuration to run the extension.

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
`api_key_config` |
Config for API key auth. This field is a member of `oneof` _ `auth_config` .
|
`http_basic_auth_config` |
Config for HTTP Basic auth. This field is a member of `oneof` _ `auth_config` .
|
`google_service_account_config` |
Config for Google Service Account auth. This field is a member of `oneof` _ `auth_config` .
|
`oauth_config` |
Config for user oauth. This field is a member of `oneof` _ `auth_config` .
|
`oidc_config` |
Config for user OIDC auth. This field is a member of `oneof` _ `auth_config` .
|
`auth_type` |
Type of auth scheme. |

## Classes

### ApiKeyConfig

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for authentication with API key.

### GoogleServiceAccountConfig

`GoogleServiceAccountConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Google Service Account Authentication.

### HttpBasicAuthConfig

`HttpBasicAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for HTTP Basic Authentication.

### OauthConfig

`OauthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user oauth.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### OidcConfig

`OidcConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user OIDC auth.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AuthConfig

`AuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Auth configuration to run the extension.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstudyspecparameterspecintegervaluespec__googleclou_4b5bed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecparameterspecintegervaluespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.IntegerValueSpec -->

# Class IntegerValueSpec (1.134.0)

`IntegerValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `INTEGER`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`min_value` |
`int`
Required. Inclusive minimum value of the parameter. |
`max_value` |
`int`
Required. Inclusive maximum value of the parameter. |
`default_value` |
`int`
A default value for an `INTEGER` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### IntegerValueSpec

`IntegerValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `INTEGER`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfulfillmentspec_googlecloudaiplatform_v1beta1_1d8916.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfulfillmentspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentSpec -->

# Class FulfillmentSpec (1.134.0)

`FulfillmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### FulfillmentSpec

`FulfillmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfullfinetunedresourcesdeploymenttype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FullFineTunedResources.DeploymentType -->

# Class DeploymentType (1.134.0)

`DeploymentType(value)`


The type of deployment.

## Enums |
|
|---|---|
Name |
Description |
`DEPLOYMENT_TYPE_UNSPECIFIED` |
Unspecified deployment type. |
`DEPLOYMENT_TYPE_EVAL` |
Eval deployment type. |
`DEPLOYMENT_TYPE_PROD` |
Prod deployment type. |

## Methods

### DeploymentType

`DeploymentType(value)`


The type of deployment.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesendpoint_serviceendpointserviceasyncclient_af909d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesendpoint_serviceendpointserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient -->

# Class EndpointServiceAsyncClient (1.134.0)

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Endpoints.

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
`EndpointServiceTransport` |
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

### EndpointServiceAsyncClient

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the endpoint service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EndpointServiceTransport,Callable[..., EndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the EndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_endpoint

```
create_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.CreateEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
endpoint_id: typing.Optional[str] = None,
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


Creates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_create_endpoint)(request=request)
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
The request object. Request message for EndpointService.CreateEndpoint. |
`parent` |
Required. The resource name of the Location to create the Endpoint in. Format: |
`endpoint` |
Required. The Endpoint to create. This corresponds to the |
`endpoint_id` |
Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are |
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

### delete_endpoint

```
delete_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.DeleteEndpointRequest,
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


Deletes an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_delete_endpoint)(request=request)
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
The request object. Request message for EndpointService.DeleteEndpoint. |
`name` |
Required. The name of the Endpoint resource to be deleted. Format: |
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

### deploy_model

```
deploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.DeployModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.DeployedModel
] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Deploys a Model into this Endpoint, creating a DeployedModel within it.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_deploy_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1beta1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_deploy_model)(request=request)
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
The request object. Request message for EndpointService.DeployModel. |
`endpoint` |
Required. The name of the Endpoint resource into which to deploy a Model. Format: |
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. This corresponds to the |
`traffic_split` |
`:class:`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. This corresponds to the |
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

### fetch_publisher_model_config

```
fetch_publisher_model_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.FetchPublisherModelConfigRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.PublisherModelConfig
```


Fetches the configs of publisher models.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_fetch_publisher_model_config():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchPublisherModelConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchPublisherModelConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[fetch_publisher_model_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_fetch_publisher_model_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.FetchPublisherModelConfig. |
`name` |
Required. The name of the publisher model, in the format of |
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
This message contains configs of a publisher model. |

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
`EndpointServiceAsyncClient` |
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
`EndpointServiceAsyncClient` |
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
`EndpointServiceAsyncClient` |
The constructed client. |

### get_endpoint

```
get_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.GetEndpointRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
```


Gets an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_get_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.GetEndpoint |
`name` |
Required. The name of the Endpoint resource. Format: |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

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
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport
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

### list_endpoints

```
list_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
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
google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager
)
```


Lists Endpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_endpoints():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_list_endpoints)(request=request)
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
The request object. Request message for EndpointService.ListEndpoints. |
`parent` |
Required. The resource name of the Location from which to list the Endpoints. Format: |
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
Response message for EndpointService.ListEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### model_deployment_monitoring_job_path

```
model_deployment_monitoring_job_path(
project: str, location: str, model_deployment_monitoring_job: str
) -> str
```


Returns a fully-qualified model_deployment_monitoring_job string.

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### mutate_deployed_model

```
mutate_deployed_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.MutateDeployedModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.DeployedModel
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


Updates an existing deployed model. Updatable fields include
`min_replica_count`

, `max_replica_count`

,
`required_replica_count`

, `autoscaling_metric_specs`

,
`disable_container_logging`

(v1 only), and
`enable_container_logging`

(v1beta1 only).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1beta1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_mutate_deployed_model)(request=request)
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
The request object. Request message for EndpointService.MutateDeployedModel. |
`endpoint` |
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: |
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - |
`update_mask` |
Required. The update mask applies to the resource. See |
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

### parse_deployment_resource_pool_path

`parse_deployment_resource_pool_path(path: str) -> typing.Dict[str, str]`


Parses a deployment_resource_pool path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_deployment_monitoring_job_path

`parse_model_deployment_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_deployment_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

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

### set_publisher_model_config

```
set_publisher_model_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.SetPublisherModelConfigRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
publisher_model_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.PublisherModelConfig
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


Sets (creates or updates) configs of publisher models. For example, sets the request/response logging config.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_set_publisher_model_config():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SetPublisherModelConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigRequest.html)(
name="name_value",
)
# Make the request
operation = client.[set_publisher_model_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_set_publisher_model_config)(request=request)
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
The request object. Request message for EndpointService.SetPublisherModelConfig. |
`name` |
Required. The name of the publisher model, in the format of |
`publisher_model_config` |
Required. The publisher model config. This corresponds to the |
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

### undeploy_model

```
undeploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UndeployModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model_id: typing.Optional[str] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_undeploy_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_undeploy_model)(request=request)
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
The request object. Request message for EndpointService.UndeployModel. |
`endpoint` |
Required. The name of the Endpoint resource from which to undeploy a Model. Format: |
`deployed_model_id` |
Required. The ID of the DeployedModel to be undeployed from the Endpoint. This corresponds to the |
`traffic_split` |
`:class:`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. This corresponds to the |
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

### update_endpoint

```
update_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UpdateEndpointRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
```


Updates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = await client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.UpdateEndpoint. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. See |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

### update_endpoint_long_running

```
update_endpoint_long_running(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UpdateEndpointLongRunningRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
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


Updates an Endpoint with a long running operation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint_long_running)(request=request)
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
The request object. Request message for EndpointService.UpdateEndpointLongRunning. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the |
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesextension_execution_serviceextensionexecut_cb2bec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesextension_execution_serviceextensionexecutionserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_execution_service.ExtensionExecutionServiceAsyncClient -->

# Class ExtensionExecutionServiceAsyncClient (1.134.0)

```
ExtensionExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.extension_execution_service.transports.base.ExtensionExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.extension_execution_service.transports.base.ExtensionExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for Extension execution.

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
`ExtensionExecutionServiceTransport` |
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

### ExtensionExecutionServiceAsyncClient

```
ExtensionExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.extension_execution_service.transports.base.ExtensionExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.extension_execution_service.transports.base.ExtensionExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the extension execution service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ExtensionExecutionServiceTransport,Callable[..., ExtensionExecutionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ExtensionExecutionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### execute_extension

```
execute_extension(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_execution_service.ExecuteExtensionRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
operation_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.extension_execution_service.ExecuteExtensionResponse
)
```


Executes the request against a given extension.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_execute_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_execution_service.ExtensionExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ExecuteExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecuteExtensionRequest.html)(
name="name_value",
operation_id="operation_id_value",
)
# Make the request
response = await client.[execute_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_execution_service.ExtensionExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_execution_service_ExtensionExecutionServiceAsyncClient_execute_extension)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExtensionExecutionService.ExecuteExtension. |
`name` |
Required. Name (identifier) of the extension; Format: |
`operation_id` |
Required. The desired ID of the operation to be executed in this extension as defined in ExtensionOperation.operation_id. This corresponds to the |
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
Response message for ExtensionExecutionService.ExecuteExtension. |

### extension_path

`extension_path(project: str, location: str, extension: str) -> str`


Returns a fully-qualified extension string.

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
`ExtensionExecutionServiceAsyncClient` |
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
`ExtensionExecutionServiceAsyncClient` |
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
`ExtensionExecutionServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.extension_execution_service.transports.base.ExtensionExecutionServiceTransport
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

### parse_extension_path

`parse_extension_path(path: str) -> typing.Dict[str, str]`


Parses a extension path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### query_extension

```
query_extension(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_execution_service.QueryExtensionRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1beta1.types.content.Content]
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
google.cloud.aiplatform_v1beta1.types.extension_execution_service.QueryExtensionResponse
)
```


Queries an extension with a default controller.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_query_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_execution_service.ExtensionExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1beta1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1beta1.[QueryExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionRequest.html)(
name="name_value",
contents=contents,
)
# Make the request
response = await client.[query_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_execution_service.ExtensionExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_execution_service_ExtensionExecutionServiceAsyncClient_query_extension)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExtensionExecutionService.QueryExtension. |
`name` |
Required. Name (identifier) of the extension; Format: |
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
Response message for ExtensionExecutionService.QueryExtension. |

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesstudyspecparameterspecdoublevaluespec__googlecl_d060e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesstudyspecparameterspecdoublevaluespec__googleclo_db4359.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstudyspecparameterspecdoublevaluespec__googleclou_066a46.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstudyspecparameterspecdoublevaluespec__googlecloud_ea21f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecparameterspecdoublevaluespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.DoubleValueSpec -->

# Class DoubleValueSpec (1.134.0)

`DoubleValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DOUBLE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`min_value` |
`float`
Required. Inclusive minimum value of the parameter. |
`max_value` |
`float`
Required. Inclusive maximum value of the parameter. |
`default_value` |
`float`
A default value for a `DOUBLE` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### DoubleValueSpec

`DoubleValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DOUBLE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfluencyinput_googlecloudaiplatform_v1typesray_99a2ad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfluencyinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencyInput -->

# Class FluencyInput (1.134.0)

`FluencyInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for fluency metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for fluency score metric. |
`instance` |
Required. Fluency instance. |

## Methods

### FluencyInput

`FluencyInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for fluency metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesraylogsspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RayLogsSpec -->

# Class RayLogsSpec (1.134.0)

`RayLogsSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray OSS Logs.

## Attribute |
|
|---|---|
Name |
Description |
`disabled` |
`bool`
Optional. Flag to disable the export of Ray OSS logs to Cloud Logging. |

## Methods

### RayLogsSpec

`RayLogsSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray OSS Logs.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespipelinetaskdetailartifactlist_googlecloudaiplatf_2e88f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespipelinetaskdetailartifactlist_googlecloudaiplatfo_f8714e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinetaskdetailartifactlist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskDetail.ArtifactList -->

# Class ArtifactList (1.134.0)

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.

## Attribute |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
Output only. A list of artifact metadata. |

## Methods

### ArtifactList

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfluencyinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FluencyInput -->

# Class FluencyInput (1.134.0)

`FluencyInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for fluency metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for fluency score metric. |
`instance` |
Required. Fluency instance. |

## Methods

### FluencyInput

`FluencyInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for fluency metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewfeatureregistrysource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.FeatureRegistrySource -->

# Class FeatureRegistrySource (1.134.0)

`FeatureRegistrySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Feature Registry source for features that need to be synced to Online Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`feature_groups` |
`MutableSequence[`
Required. List of features that need to be synced to Online Store. |
`project_number` |
`int`
Optional. The project number of the parent project of the Feature Groups. This field is a member of `oneof` _ `_project_number` .
|

## Classes

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

## Methods

### FeatureRegistrySource

`FeatureRegistrySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Feature Registry source for features that need to be synced to Online Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeatureviewfeatureregistrysource_googlecloud_133f1c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewfeatureregistrysource_googleclouda_97352b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewfeatureregistrysource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.FeatureRegistrySource -->

# Class FeatureRegistrySource (1.134.0)

`FeatureRegistrySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Feature Registry source for features that need to be synced to Online Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`feature_groups` |
`MutableSequence[`
Required. List of features that need to be synced to Online Store. |
`project_number` |
`int`
Optional. The project number of the parent project of the Feature Groups. This field is a member of `oneof` _ `_project_number` .
|

## Classes

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

## Methods

### FeatureRegistrySource

`FeatureRegistrySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Feature Registry source for features that need to be synced to Online Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecparameterspecintegervaluespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.IntegerValueSpec -->

# Class IntegerValueSpec (1.134.0)

`IntegerValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `INTEGER`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`min_value` |
`int`
Required. Inclusive minimum value of the parameter. |
`max_value` |
`int`
Required. Inclusive maximum value of the parameter. |
`default_value` |
`int`
A default value for an `INTEGER` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### IntegerValueSpec

`IntegerValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `INTEGER`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringbigquerytablelogtyp_dd25ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringbigquerytablelogtype_07661b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringbigquerytablelogtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringBigQueryTable.LogType -->

# Class LogType (1.134.0)

`LogType(value)`


Indicates what type of traffic does the log belong to.

## Enums |
|
|---|---|
Name |
Description |
`LOG_TYPE_UNSPECIFIED` |
Unspecified type. |
`PREDICT` |
Predict logs. |
`EXPLAIN` |
Explain logs. |

## Methods

### LogType

`LogType(value)`


Indicates what type of traffic does the log belong to.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdynamicretrievalconfigmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DynamicRetrievalConfig.Mode -->

# Class Mode (1.134.0)

`Mode(value)`


The mode of the predictor to be used in dynamic retrieval.

## Enums |
|
|---|---|
Name |
Description |
`MODE_UNSPECIFIED` |
Always trigger retrieval. |
`MODE_DYNAMIC` |
Run retrieval only when system decides it is necessary. |

## Methods

### Mode

`Mode(value)`


The mode of the predictor to be used in dynamic retrieval.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexecutablecodelanguage_googlecloudaiplatform_v1typ_728b16.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexecutablecodelanguage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExecutableCode.Language -->

# Class Language (1.134.0)

`Language(value)`


Supported programming languages for the generated code.

## Enums |
|
|---|---|
Name |
Description |
`LANGUAGE_UNSPECIFIED` |
Unspecified language. This value should not be used. |
`PYTHON` |
Python >= 3.10, with numpy and simpy available. |

## Methods

### Language

`Language(value)`


Supported programming languages for the generated code.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolcomputeruseenvironment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.ComputerUse.Environment -->

# Class Environment (1.134.0)

`Environment(value)`


Represents the environment being operated, such as a web browser.

## Enums |
|
|---|---|
Name |
Description |
`ENVIRONMENT_UNSPECIFIED` |
Defaults to browser. |
`ENVIRONMENT_BROWSER` |
Operates in a web browser. |

## Methods

### Environment

`Environment(value)`


Represents the environment being operated, such as a web browser.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesoutputfieldspecfieldtype_googlecloudaiplatform__8ed5bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesoutputfieldspecfieldtype_googlecloudaiplatform_v_4c98ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesoutputfieldspecfieldtype_googlecloudaiplatform_v1_163b0c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesoutputfieldspecfieldtype_googlecloudaiplatform_v1t_38505e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesoutputfieldspecfieldtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.OutputFieldSpec.FieldType -->

# Class FieldType (1.134.0)

`FieldType(value)`


The data type of the field.

## Enums |
|
|---|---|
Name |
Description |
`FIELD_TYPE_UNSPECIFIED` |
Field type is unspecified. |
`CONTENT` |
Arbitrary content field type. |
`TEXT` |
Text field type. |
`IMAGE` |
Image field type. |
`AUDIO` |
Audio field type. |

## Methods

### FieldType

`FieldType(value)`


The data type of the field.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadfeaturevaluesresponsefeaturedescriptor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesResponse.FeatureDescriptor -->

# Class FeatureDescriptor (1.134.0)

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.

## Attribute |
|
|---|---|
Name |
Description |
`id` |
`str`
Feature ID. |

## Methods

### FeatureDescriptor

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeswritefeaturevaluespayload.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesPayload -->

# Class WriteFeatureValuesPayload (1.134.0)

`WriteFeatureValuesPayload(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains Feature values to be written for a specific entity.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
Required. The ID of the entity. |
`feature_values` |
`MutableMapping[str, `
Required. Feature values to be written, mapping from Feature ID to value. Up to 100,000 `feature_values` entries may be
written across all payloads. The feature generation time,
aligned by days, must be no older than five years (1825
days) and no later than one year (366 days) in the future.
|

## Classes

### FeatureValuesEntry

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### WriteFeatureValuesPayload

`WriteFeatureValuesPayload(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains Feature values to be written for a specific entity.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelevaluationslicesliceslicespecvalue_googleclou_4005e7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelevaluationslicesliceslicespecvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.Value -->

# Class Value (1.134.0)

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Single value that supports strings and floats.

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
`string_value` |
`str`
String type. This field is a member of `oneof` _ `kind` .
|
`float_value` |
`float`
Float type. This field is a member of `oneof` _ `kind` .
|

## Methods

### Value

`Value(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Single value that supports strings and floats.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureOnlineStoreRequest -->

# Class UpdateFeatureOnlineStoreRequest (1.134.0)

```
UpdateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_store` |
Required. The FeatureOnlineStore's `name` field is used to
identify the FeatureOnlineStore to be updated. Format:
`projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureOnlineStore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `description`
- `bigtable`
- `bigtable.auto_scaling`
- `bigtable.enable_multi_region_replica`
|

## Methods

### UpdateFeatureOnlineStoreRequest

```
UpdateFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesbatchmigrateresourcesoperationmetadata__googleclo_7895a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchmigrateresourcesoperationmetadata__googleclou_847fef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchmigrateresourcesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesOperationMetadata -->

# Class BatchMigrateResourcesOperationMetadata (1.134.0)

```
BatchMigrateResourcesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for MigrationService.BatchMigrateResources.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`partial_results` |
`MutableSequence[`
Partial results that reflect the latest migration operation progress. |

## Classes

### PartialResult

`PartialResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a partial result in batch migration operation for one MigrateResourceRequest.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### BatchMigrateResourcesOperationMetadata

```
BatchMigrateResourcesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for MigrationService.BatchMigrateResources.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescontentmapcontents_googlecloudaiplatform_v1be_10dbca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontentmapcontents.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContentMap.Contents -->

# Class Contents (1.134.0)

`Contents(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Repeated Content type.

## Attribute |
|
|---|---|
Name |
Description |
`contents` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.Content]`
Optional. Repeated contents. |

## Methods

### Contents

`Contents(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Repeated Content type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexecutablecodelanguage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecutableCode.Language -->

# Class Language (1.134.0)

`Language(value)`


Supported programming languages for the generated code.

## Enums |
|
|---|---|
Name |
Description |
`LANGUAGE_UNSPECIFIED` |
Unspecified language. This value should not be used. |
`PYTHON` |
Python >= 3.10, with numpy and simpy available. |

## Methods

### Language

`Language(value)`


Supported programming languages for the generated code.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespredictlongrunningmetadata_googlecloudaiplat_9355fe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespredictlongrunningmetadata_googlecloudaiplatf_05e881.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespredictlongrunningmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictLongRunningMetadata -->

# Class PredictLongRunningMetadata (1.134.0)

`PredictLongRunningMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for PredictLongRunning long running operations.

## Methods

### PredictLongRunningMetadata

`PredictLongRunningMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for PredictLongRunning long running operations.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesaddexecutioneventsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddExecutionEventsResponse -->

# Class AddExecutionEventsResponse (1.134.0)

`AddExecutionEventsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.AddExecutionEvents.

## Methods

### AddExecutionEventsResponse

`AddExecutionEventsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.AddExecutionEvents.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstopnotebookruntimeresponse_googlecloudaiplat_b8873d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstopnotebookruntimeresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeResponse -->

# Class StopNotebookRuntimeResponse (1.134.0)

`StopNotebookRuntimeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for NotebookService.StopNotebookRuntime.

## Methods

### StopNotebookRuntimeResponse

`StopNotebookRuntimeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for NotebookService.StopNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundednessspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundednessSpec -->

# Class GroundednessSpec (1.134.0)

`GroundednessSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### GroundednessSpec

`GroundednessSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicestensorboard_servicetensorboardserviceasync_b7c0b1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicetensorboardserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient -->

# Class TensorboardServiceAsyncClient (1.134.0)

```
TensorboardServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### TensorboardServiceAsyncClient

```
TensorboardServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the tensorboard service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the TensorboardServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_create_tensorboard_runs

```
batch_create_tensorboard_runs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.BatchCreateTensorboardRunsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.CreateTensorboardRunRequest
]
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
google.cloud.aiplatform_v1beta1.types.tensorboard_service.BatchCreateTensorboardRunsResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_batch_create_tensorboard_runs():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardRunRequest.html)()
requests.parent = "parent_value"
requests.tensorboard_run.display_name = "display_name_value"
requests.tensorboard_run_id = "tensorboard_run_id_value"
request = aiplatform_v1beta1.[BatchCreateTensorboardRunsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardRunsRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
response = await client.[batch_create_tensorboard_runs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_batch_create_tensorboard_runs)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.BatchCreateTensorboardRuns. |
`parent` |
Required. The resource name of the TensorboardExperiment to create the TensorboardRuns in. Format: |
`requests` |
`:class:`
Required. The request message specifying the TensorboardRuns to create. A maximum of 1000 TensorboardRuns can be created in a batch. This corresponds to the |
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
Response message for TensorboardService.BatchCreateTensorboardRuns. |

### batch_create_tensorboard_time_series

```
batch_create_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.BatchCreateTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.CreateTensorboardTimeSeriesRequest
]
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
google.cloud.aiplatform_v1beta1.types.tensorboard_service.BatchCreateTensorboardTimeSeriesResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_batch_create_tensorboard_time_series():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardTimeSeriesRequest.html)()
requests.parent = "parent_value"
requests.tensorboard_time_series.display_name = "display_name_value"
requests.tensorboard_time_series.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1beta1.[BatchCreateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardTimeSeriesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
response = await client.[batch_create_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_batch_create_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.BatchCreateTensorboardTimeSeries. |
`parent` |
Required. The resource name of the TensorboardExperiment to create the TensorboardTimeSeries in. Format: |
`requests` |
`:class:`
Required. The request message specifying the TensorboardTimeSeries to create. A maximum of 1000 TensorboardTimeSeries can be created in a batch. This corresponds to the |
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
Response message for TensorboardService.BatchCreateTensorboardTimeSeries. |

### batch_read_tensorboard_time_series_data

```
batch_read_tensorboard_time_series_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.BatchReadTensorboardTimeSeriesDataRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.tensorboard_service.BatchReadTensorboardTimeSeriesDataResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_batch_read_tensorboard_time_series_data():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchReadTensorboardTimeSeriesDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadTensorboardTimeSeriesDataRequest.html)(
tensorboard="tensorboard_value",
time_series=['time_series_value1', 'time_series_value2'],
)
# Make the request
response = await client.[batch_read_tensorboard_time_series_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_batch_read_tensorboard_time_series_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.BatchReadTensorboardTimeSeriesData. |
`tensorboard` |
Required. The resource name of the Tensorboard containing TensorboardTimeSeries to read data from. Format: |
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

### create_tensorboard

```
create_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.CreateTensorboardRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard.Tensorboard
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


Creates a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_tensorboard():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
tensorboard = aiplatform_v1beta1.[Tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensorboard.html)()
tensorboard.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardRequest.html)(
parent="parent_value",
tensorboard=tensorboard,
)
# Make the request
operation = client.[create_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_create_tensorboard)(request=request)
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
The request object. Request message for TensorboardService.CreateTensorboard. |
`parent` |
Required. The resource name of the Location to create the Tensorboard in. Format: |
`tensorboard` |
Required. The Tensorboard to create. This corresponds to the |
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

### create_tensorboard_experiment

```
create_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.CreateTensorboardExperimentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard_experiment: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard_experiment.TensorboardExperiment
] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.tensorboard_experiment.TensorboardExperiment
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
from google.cloud import aiplatform_v1beta1
async def sample_create_tensorboard_experiment():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardExperimentRequest.html)(
parent="parent_value",
tensorboard_experiment_id="tensorboard_experiment_id_value",
)
# Make the request
response = await client.[create_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_create_tensorboard_experiment)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.CreateTensorboardExperiment. |
`parent` |
Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: |
`tensorboard_experiment` |
The TensorboardExperiment to create. This corresponds to the |
`tensorboard_experiment_id` |
Required. The ID to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are |
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
A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard. |

### create_tensorboard_run

```
create_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.CreateTensorboardRunRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard_run: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard_run.TensorboardRun
] = None,
tensorboard_run_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.tensorboard_run.TensorboardRun
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
from google.cloud import aiplatform_v1beta1
async def sample_create_tensorboard_run():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
tensorboard_run = aiplatform_v1beta1.[TensorboardRun](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardRun.html)()
tensorboard_run.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardRunRequest.html)(
parent="parent_value",
tensorboard_run=tensorboard_run,
tensorboard_run_id="tensorboard_run_id_value",
)
# Make the request
response = await client.[create_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_create_tensorboard_run)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.CreateTensorboardRun. |
`parent` |
Required. The resource name of the TensorboardExperiment to create the TensorboardRun in. Format: |
`tensorboard_run` |
Required. The TensorboardRun to create. This corresponds to the |
`tensorboard_run_id` |
Required. The ID to use for the Tensorboard run, which becomes the final component of the Tensorboard run's resource name. This value should be 1-128 characters, and valid characters are |
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
TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc |

### create_tensorboard_time_series

```
create_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.CreateTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard_time_series: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard_time_series.TensorboardTimeSeries
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
google.cloud.aiplatform_v1beta1.types.tensorboard_time_series.TensorboardTimeSeries
)
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
from google.cloud import aiplatform_v1beta1
async def sample_create_tensorboard_time_series():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
tensorboard_time_series = aiplatform_v1beta1.[TensorboardTimeSeries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries.html)()
tensorboard_time_series.display_name = "display_name_value"
tensorboard_time_series.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1beta1.[CreateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardTimeSeriesRequest.html)(
parent="parent_value",
tensorboard_time_series=tensorboard_time_series,
)
# Make the request
response = await client.[create_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_create_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.CreateTensorboardTimeSeries. |
`parent` |
Required. The resource name of the TensorboardRun to create the TensorboardTimeSeries in. Format: |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries to create. This corresponds to the |
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

### delete_tensorboard

```
delete_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.DeleteTensorboardRequest,
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


Deletes a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_tensorboard():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_delete_tensorboard)(request=request)
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
The request object. Request message for TensorboardService.DeleteTensorboard. |
`name` |
Required. The name of the Tensorboard to be deleted. Format: |
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

### delete_tensorboard_experiment

```
delete_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.DeleteTensorboardExperimentRequest,
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


Deletes a TensorboardExperiment.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_tensorboard_experiment():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardExperimentRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_delete_tensorboard_experiment)(request=request)
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
The request object. Request message for TensorboardService.DeleteTensorboardExperiment. |
`name` |
Required. The name of the TensorboardExperiment to be deleted. Format: |
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

### delete_tensorboard_run

```
delete_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.DeleteTensorboardRunRequest,
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


Deletes a TensorboardRun.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_tensorboard_run():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRunRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_delete_tensorboard_run)(request=request)
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
The request object. Request message for TensorboardService.DeleteTensorboardRun. |
`name` |
Required. The name of the TensorboardRun to be deleted. Format: |
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

### delete_tensorboard_time_series

```
delete_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.DeleteTensorboardTimeSeriesRequest,
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


Deletes a TensorboardTimeSeries.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_tensorboard_time_series():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardTimeSeriesRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_delete_tensorboard_time_series)(request=request)
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
The request object. Request message for TensorboardService.DeleteTensorboardTimeSeries. |
`name` |
Required. The name of the TensorboardTimeSeries to be deleted. Format: |
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

### export_tensorboard_time_series_data

```
export_tensorboard_time_series_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
dict,
]
] = None,
*,
tensorboard_time_series: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_export_tensorboard_time_series_data():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ExportTensorboardTimeSeriesDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataRequest.html)(
tensorboard_time_series="tensorboard_time_series_value",
)
# Make the request
page_result = client.[export_tensorboard_time_series_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_export_tensorboard_time_series_data)(request=request)
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
The request object. Request message for TensorboardService.ExportTensorboardTimeSeriesData. |
`tensorboard_time_series` |
Required. The resource name of the TensorboardTimeSeries to export data from. Format: |
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
`TensorboardServiceAsyncClient` |
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
`TensorboardServiceAsyncClient` |
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
`TensorboardServiceAsyncClient` |
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

### get_tensorboard

```
get_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.GetTensorboardRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.tensorboard.Tensorboard
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
from google.cloud import aiplatform_v1beta1
async def sample_get_tensorboard():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_get_tensorboard)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.GetTensorboard. |
`name` |
Required. The name of the Tensorboard resource. Format: |
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
Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects. |

### get_tensorboard_experiment

```
get_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.GetTensorboardExperimentRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.tensorboard_experiment.TensorboardExperiment
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
from google.cloud import aiplatform_v1beta1
async def sample_get_tensorboard_experiment():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardExperimentRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_get_tensorboard_experiment)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.GetTensorboardExperiment. |
`name` |
Required. The name of the TensorboardExperiment resource. Format: |
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
A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard. |

### get_tensorboard_run

```
get_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.GetTensorboardRunRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.tensorboard_run.TensorboardRun
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
from google.cloud import aiplatform_v1beta1
async def sample_get_tensorboard_run():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardRunRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_get_tensorboard_run)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.GetTensorboardRun. |
`name` |
Required. The name of the TensorboardRun resource. Format: |
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
TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc |

### get_tensorboard_time_series

```
get_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.GetTensorboardTimeSeriesRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.types.tensorboard_time_series.TensorboardTimeSeries
)
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
from google.cloud import aiplatform_v1beta1
async def sample_get_tensorboard_time_series():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardTimeSeriesRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_get_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.GetTensorboardTimeSeries. |
`name` |
Required. The name of the TensorboardTimeSeries resource. Format: |
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
TensorboardTimeSeries maps to times series produced in training runs |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.tensorboard_service.transports.base.TensorboardServiceTransport
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

### list_tensorboard_experiments

```
list_tensorboard_experiments(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
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
google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardExperimentsAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_tensorboard_experiments():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTensorboardExperimentsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboard_experiments](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_list_tensorboard_experiments)(request=request)
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
The request object. Request message for TensorboardService.ListTensorboardExperiments. |
`parent` |
Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: |
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
Response message for TensorboardService.ListTensorboardExperiments. Iterating over this object will yield results and resolve additional pages automatically. |

### list_tensorboard_runs

```
list_tensorboard_runs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
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
google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardRunsAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_tensorboard_runs():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTensorboardRunsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboard_runs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_list_tensorboard_runs)(request=request)
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
The request object. Request message for TensorboardService.ListTensorboardRuns. |
`parent` |
Required. The resource name of the TensorboardExperiment to list TensorboardRuns. Format: |
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
Response message for TensorboardService.ListTensorboardRuns. Iterating over this object will yield results and resolve additional pages automatically. |

### list_tensorboard_time_series

```
list_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
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
google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_tensorboard_time_series():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_list_tensorboard_time_series)(request=request)
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
The request object. Request message for TensorboardService.ListTensorboardTimeSeries. |
`parent` |
Required. The resource name of the TensorboardRun to list TensorboardTimeSeries. Format: |
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
Response message for TensorboardService.ListTensorboardTimeSeries. Iterating over this object will yield results and resolve additional pages automatically. |

### list_tensorboards

```
list_tensorboards(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
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
google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardsAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_tensorboards():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTensorboardsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboards](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_list_tensorboards)(request=request)
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
The request object. Request message for TensorboardService.ListTensorboards. |
`parent` |
Required. The resource name of the Location to list Tensorboards. Format: |
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
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardBlobDataRequest,
dict,
]
] = None,
*,
time_series: typing.Optional[str] = None,
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
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardBlobDataResponse
]
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
from google.cloud import aiplatform_v1beta1
async def sample_read_tensorboard_blob_data():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadTensorboardBlobDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataRequest.html)(
time_series="time_series_value",
)
# Make the request
stream = await client.[read_tensorboard_blob_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_read_tensorboard_blob_data)(request=request)
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
The request object. Request message for TensorboardService.ReadTensorboardBlobData. |
`time_series` |
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: |
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
Response message for TensorboardService.ReadTensorboardBlobData. |

### read_tensorboard_size

```
read_tensorboard_size(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardSizeRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardSizeResponse
)
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
from google.cloud import aiplatform_v1beta1
async def sample_read_tensorboard_size():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadTensorboardSizeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardSizeRequest.html)(
tensorboard="tensorboard_value",
)
# Make the request
response = await client.[read_tensorboard_size](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_read_tensorboard_size)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.ReadTensorboardSize. |
`tensorboard` |
Required. The name of the Tensorboard resource. Format: |
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
Response message for TensorboardService.ReadTensorboardSize. |

### read_tensorboard_time_series_data

```
read_tensorboard_time_series_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardTimeSeriesDataRequest,
dict,
]
] = None,
*,
tensorboard_time_series: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardTimeSeriesDataResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_read_tensorboard_time_series_data():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadTensorboardTimeSeriesDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardTimeSeriesDataRequest.html)(
tensorboard_time_series="tensorboard_time_series_value",
)
# Make the request
response = await client.[read_tensorboard_time_series_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_read_tensorboard_time_series_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.ReadTensorboardTimeSeriesData. |
`tensorboard_time_series` |
Required. The resource name of the TensorboardTimeSeries to read data from. Format: |
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
Response message for TensorboardService.ReadTensorboardTimeSeriesData. |

### read_tensorboard_usage

```
read_tensorboard_usage(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardUsageRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ReadTensorboardUsageResponse
)
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
from google.cloud import aiplatform_v1beta1
async def sample_read_tensorboard_usage():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadTensorboardUsageRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageRequest.html)(
tensorboard="tensorboard_value",
)
# Make the request
response = await client.[read_tensorboard_usage](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_read_tensorboard_usage)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.ReadTensorboardUsage. |
`tensorboard` |
Required. The name of the Tensorboard resource. Format: |
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
Response message for TensorboardService.ReadTensorboardUsage. |

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

### update_tensorboard

```
update_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.UpdateTensorboardRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard.Tensorboard
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


Updates a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_tensorboard():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
tensorboard = aiplatform_v1beta1.[Tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensorboard.html)()
tensorboard.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRequest.html)(
tensorboard=tensorboard,
)
# Make the request
operation = client.[update_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_update_tensorboard)(request=request)
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
The request object. Request message for TensorboardService.UpdateTensorboard. |
`tensorboard` |
Required. The Tensorboard's |
`update_mask` |
Required. Field mask is used to specify the fields to be overwritten in the Tensorboard resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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

### update_tensorboard_experiment

```
update_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.UpdateTensorboardExperimentRequest,
dict,
]
] = None,
*,
tensorboard_experiment: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard_experiment.TensorboardExperiment
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
) -> google.cloud.aiplatform_v1beta1.types.tensorboard_experiment.TensorboardExperiment
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
from google.cloud import aiplatform_v1beta1
async def sample_update_tensorboard_experiment():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardExperimentRequest.html)(
)
# Make the request
response = await client.[update_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_update_tensorboard_experiment)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.UpdateTensorboardExperiment. |
`tensorboard_experiment` |
Required. The TensorboardExperiment's |
`update_mask` |
Required. Field mask is used to specify the fields to be overwritten in the TensorboardExperiment resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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
A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard. |

### update_tensorboard_run

```
update_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.UpdateTensorboardRunRequest,
dict,
]
] = None,
*,
tensorboard_run: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard_run.TensorboardRun
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
) -> google.cloud.aiplatform_v1beta1.types.tensorboard_run.TensorboardRun
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
from google.cloud import aiplatform_v1beta1
async def sample_update_tensorboard_run():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
tensorboard_run = aiplatform_v1beta1.[TensorboardRun](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardRun.html)()
tensorboard_run.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRunRequest.html)(
tensorboard_run=tensorboard_run,
)
# Make the request
response = await client.[update_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_update_tensorboard_run)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.UpdateTensorboardRun. |
`tensorboard_run` |
Required. The TensorboardRun's |
`update_mask` |
Required. Field mask is used to specify the fields to be overwritten in the TensorboardRun resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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
TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc |

### update_tensorboard_time_series

```
update_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.UpdateTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
tensorboard_time_series: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tensorboard_time_series.TensorboardTimeSeries
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
) -> (
google.cloud.aiplatform_v1beta1.types.tensorboard_time_series.TensorboardTimeSeries
)
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
from google.cloud import aiplatform_v1beta1
async def sample_update_tensorboard_time_series():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
tensorboard_time_series = aiplatform_v1beta1.[TensorboardTimeSeries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries.html)()
tensorboard_time_series.display_name = "display_name_value"
tensorboard_time_series.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1beta1.[UpdateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardTimeSeriesRequest.html)(
tensorboard_time_series=tensorboard_time_series,
)
# Make the request
response = await client.[update_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_update_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.UpdateTensorboardTimeSeries. |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries' |
`update_mask` |
Required. Field mask is used to specify the fields to be overwritten in the TensorboardTimeSeries resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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

### write_tensorboard_experiment_data

```
write_tensorboard_experiment_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.WriteTensorboardExperimentDataRequest,
dict,
]
] = None,
*,
tensorboard_experiment: typing.Optional[str] = None,
write_run_data_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.WriteTensorboardRunDataRequest
]
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
google.cloud.aiplatform_v1beta1.types.tensorboard_service.WriteTensorboardExperimentDataResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_write_tensorboard_experiment_data():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
write_run_data_requests = aiplatform_v1beta1.[WriteTensorboardRunDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardRunDataRequest.html)()
write_run_data_requests.tensorboard_run = "tensorboard_run_value"
write_run_data_requests.time_series_data.tensorboard_time_series_id = "tensorboard_time_series_id_value"
write_run_data_requests.time_series_data.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1beta1.[WriteTensorboardExperimentDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardExperimentDataRequest.html)(
tensorboard_experiment="tensorboard_experiment_value",
write_run_data_requests=write_run_data_requests,
)
# Make the request
response = await client.[write_tensorboard_experiment_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_write_tensorboard_experiment_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.WriteTensorboardExperimentData. |
`tensorboard_experiment` |
Required. The resource name of the TensorboardExperiment to write data to. Format: |
`write_run_data_requests` |
`:class:`
Required. Requests containing per-run TensorboardTimeSeries data to write. This corresponds to the |
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
Response message for TensorboardService.WriteTensorboardExperimentData. |

### write_tensorboard_run_data

```
write_tensorboard_run_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.WriteTensorboardRunDataRequest,
dict,
]
] = None,
*,
tensorboard_run: typing.Optional[str] = None,
time_series_data: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.tensorboard_data.TimeSeriesData
]
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
google.cloud.aiplatform_v1beta1.types.tensorboard_service.WriteTensorboardRunDataResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_write_tensorboard_run_data():
# Create a client
client = aiplatform_v1beta1.
```[TensorboardServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html)()
# Initialize request argument(s)
time_series_data = aiplatform_v1beta1.[TimeSeriesData](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimeSeriesData.html)()
time_series_data.tensorboard_time_series_id = "tensorboard_time_series_id_value"
time_series_data.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1beta1.[WriteTensorboardRunDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardRunDataRequest.html)(
tensorboard_run="tensorboard_run_value",
time_series_data=time_series_data,
)
# Make the request
response = await client.[write_tensorboard_run_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_tensorboard_service_TensorboardServiceAsyncClient_write_tensorboard_run_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for TensorboardService.WriteTensorboardRunData. |
`tensorboard_run` |
Required. The resource name of the TensorboardRun to write data to. Format: |
`time_series_data` |
`:class:`
Required. The TensorboardTimeSeries data to write. Values with in a time series are indexed by their step value. Repeated writes to the same step will overwrite the existing value for that step. The upper limit of data points per write request is 5000. This corresponds to the |
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
Response message for TensorboardService.WriteTensorboardRunData. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesvertex_rag_data_servicevertexragdataserviceasyn_70fdee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_servicevertexragdataserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient -->

# Class VertexRagDataServiceAsyncClient (1.134.0)

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing user data for RAG.

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
`VertexRagDataServiceTransport` |
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

### VertexRagDataServiceAsyncClient

```
VertexRagDataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag data service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagDataServiceTransport,Callable[..., VertexRagDataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagDataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_rag_corpus

```
create_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.CreateRagCorpusRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_data.RagCorpus
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


Creates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_rag_corpus():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1.[CreateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateRagCorpusRequest.html)(
parent="parent_value",
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[create_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_create_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.CreateRagCorpus. |
`parent` |
Required. The resource name of the Location to create the RagCorpus in. Format: |
`rag_corpus` |
Required. The RagCorpus to create. This corresponds to the |
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

### delete_rag_corpus

```
delete_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.DeleteRagCorpusRequest,
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


Deletes a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_rag_corpus():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteRagCorpusRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagCorpus. |
`name` |
Required. The name of the RagCorpus resource to be deleted. Format: |
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

### delete_rag_file

```
delete_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.DeleteRagFileRequest,
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


Deletes a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_rag_file():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteRagFileRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_delete_rag_file)(request=request)
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
The request object. Request message for VertexRagDataService.DeleteRagFile. |
`name` |
Required. The name of the RagFile resource to be deleted. Format: |
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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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
`VertexRagDataServiceAsyncClient` |
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

### get_rag_corpus

```
get_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.GetRagCorpusRequest,
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
) -> google.cloud.aiplatform_v1.types.vertex_rag_data.RagCorpus
```


Gets a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_rag_corpus():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagCorpusRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_corpus)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagCorpus |
`name` |
Required. The name of the RagCorpus resource. Format: |
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
A RagCorpus is a RagFile container and a project can have multiple RagCorpora. |

### get_rag_engine_config

```
get_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.GetRagEngineConfigRequest,
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
) -> google.cloud.aiplatform_v1.types.vertex_rag_data.RagEngineConfig
```


Gets a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_rag_engine_config():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagEngineConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_engine_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagEngineConfig |
`name` |
Required. The name of the RagEngineConfig resource. Format: |
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
Config for RagEngine. |

### get_rag_file

```
get_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.GetRagFileRequest,
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
) -> google.cloud.aiplatform_v1.types.vertex_rag_data.RagFile
```


Gets a RagFile.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_rag_file():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagFileRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_get_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.GetRagFile |
`name` |
Required. The name of the RagFile resource. Format: |
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
A RagFile contains user data for chunking, embedding and indexing. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.vertex_rag_data_service.transports.base.VertexRagDataServiceTransport
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

### import_rag_files

```
import_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ImportRagFilesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
import_rag_files_config: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_data.ImportRagFilesConfig
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


Import files from Google Cloud Storage or Google Drive into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_import_rag_files():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
import_rag_files_config = aiplatform_v1.[ImportRagFilesConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportRagFilesConfig.html)()
import_rag_files_config.gcs_source.uris = ['uris_value1', 'uris_value2']
import_rag_files_config.partial_failure_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
import_rag_files_config.import_result_gcs_sink.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1.[ImportRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportRagFilesRequest.html)(
parent="parent_value",
import_rag_files_config=import_rag_files_config,
)
# Make the request
operation = client.[import_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_import_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ImportRagFiles. |
`parent` |
Required. The name of the RagCorpus resource into which to import files. Format: |
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. This corresponds to the |
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

### list_rag_corpora

```
list_rag_corpora(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
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
google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager
)
```


Lists RagCorpora in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_rag_corpora():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListRagCorporaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_corpora](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_corpora)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagCorpora. |
`parent` |
Required. The resource name of the Location from which to list the RagCorpora. Format: |
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
Response message for VertexRagDataService.ListRagCorpora. Iterating over this object will yield results and resolve additional pages automatically. |

### list_rag_files

```
list_rag_files(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
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
google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager
)
```


Lists RagFiles in a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_rag_files():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListRagFilesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_rag_files](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_list_rag_files)(request=request)
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
The request object. Request message for VertexRagDataService.ListRagFiles. |
`parent` |
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: |
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
Response message for VertexRagDataService.ListRagFiles. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_rag_engine_config_path

`parse_rag_engine_config_path(path: str) -> typing.Dict[str, str]`


Parses a rag_engine_config path into its component segments.

### parse_rag_file_path

`parse_rag_file_path(path: str) -> typing.Dict[str, str]`


Parses a rag_file path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### rag_engine_config_path

`rag_engine_config_path(project: str, location: str) -> str`


Returns a fully-qualified rag_engine_config string.

### rag_file_path

`rag_file_path(project: str, location: str, rag_corpus: str, rag_file: str) -> str`


Returns a fully-qualified rag_file string.

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

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

### update_rag_corpus

```
update_rag_corpus(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.UpdateRagCorpusRequest,
dict,
]
] = None,
*,
rag_corpus: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_data.RagCorpus
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


Updates a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_rag_corpus():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_corpus = aiplatform_v1.[RagCorpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagCorpus.html)()
rag_corpus.display_name = "display_name_value"
request = aiplatform_v1.[UpdateRagCorpusRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateRagCorpusRequest.html)(
rag_corpus=rag_corpus,
)
# Make the request
operation = client.[update_rag_corpus](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_corpus)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagCorpus. |
`rag_corpus` |
Required. The RagCorpus which replaces the resource on the server. This corresponds to the |
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

### update_rag_engine_config

```
update_rag_engine_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.UpdateRagEngineConfigRequest,
dict,
]
] = None,
*,
rag_engine_config: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_data.RagEngineConfig
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


Updates a RagEngineConfig.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_rag_engine_config():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateRagEngineConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateRagEngineConfigRequest.html)(
)
# Make the request
operation = client.[update_rag_engine_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_update_rag_engine_config)(request=request)
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
The request object. Request message for VertexRagDataService.UpdateRagEngineConfig. |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. This corresponds to the |
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

### upload_rag_file

```
upload_rag_file(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.UploadRagFileRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
rag_file: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_data.RagFile
] = None,
upload_rag_file_config: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_data.UploadRagFileConfig
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_data_service.UploadRagFileResponse
```


Upload a file into a RagCorpus.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_upload_rag_file():
# Create a client
client = aiplatform_v1.
```[VertexRagDataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html)()
# Initialize request argument(s)
rag_file = aiplatform_v1.[RagFile](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFile.html)()
rag_file.gcs_source.uris = ['uris_value1', 'uris_value2']
rag_file.display_name = "display_name_value"
request = aiplatform_v1.[UploadRagFileRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileRequest.html)(
parent="parent_value",
rag_file=rag_file,
)
# Make the request
response = await client.[upload_rag_file](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_data_service_VertexRagDataServiceAsyncClient_upload_rag_file)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagDataService.UploadRagFile. |
`parent` |
Required. The name of the RagCorpus resource into which to upload the file. Format: |
`rag_file` |
Required. The RagFile to upload. This corresponds to the |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. This corresponds to the |
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
Response message for VertexRagDataService.UploadRagFile. |

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesreasoning_engine_execution_servicereasoningengi_f9acc4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesreasoning_engine_execution_servicereasoningengineexecutionserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient -->

# Class ReasoningEngineExecutionServiceAsyncClient (1.134.0)

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for executing queries on Reasoning Engine.

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
`ReasoningEngineExecutionServiceTransport` |
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

### ReasoningEngineExecutionServiceAsyncClient

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine execution service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineExecutionServiceTransport,Callable[..., ReasoningEngineExecutionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineExecutionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport
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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### query_reasoning_engine

```
query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_execution_service.QueryReasoningEngineRequest,
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
google.cloud.aiplatform_v1.types.reasoning_engine_execution_service.QueryReasoningEngineResponse
)
```


Queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_query_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_query_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.Query][]. |
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
Response message for [ReasoningEngineExecutionService.Query][] |

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

### stream_query_reasoning_engine

```
stream_query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_execution_service.StreamQueryReasoningEngineRequest,
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
) -> typing.Awaitable[typing.AsyncIterable[google.api.httpbody_pb2.HttpBody]]
```


Streams queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stream_query_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamQueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamQueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
stream = await client.[stream_query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_stream_query_reasoning_engine)(request=request)
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
The request object. Request message for [ReasoningEngineExecutionService.StreamQuery][]. |
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesfeatureonlinestorededicatedservingendpoint_1c823b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesfeatureonlinestorededicatedservingendpoint__82eec2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeatureonlinestorededicatedservingendpoint_g_a35a9b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureonlinestorededicatedservingendpoint_go_2320d3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestorededicatedservingendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.DedicatedServingEndpoint -->

# Class DedicatedServingEndpoint (1.134.0)

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.

## Attributes |
|
|---|---|
Name |
Description |
`public_endpoint_domain_name` |
`str`
Output only. This field will be populated with the domain name to use for this FeatureOnlineStore |
`private_service_connect_config` |
Optional. Private service connect config. The private service connection is available only for Optimized storage type, not for embedding management now. If PrivateServiceConnectConfig.enable_private_service_connect set to true, customers will use private service connection to send request. Otherwise, the connection will set to public endpoint. |
`service_attachment` |
`str`
Output only. The name of the service attachment resource. Populated if private service connect is enabled and after FeatureViewSync is created. |

## Methods

### DedicatedServingEndpoint

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmachinespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MachineSpec -->

# Class MachineSpec (1.134.0)

`MachineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a single machine.

## Attributes |
|
|---|---|
Name |
Description |
`machine_type` |
`str`
Immutable. The type of the machine. See the `list of machine types supported for prediction |
`accelerator_type` |
Immutable. The type of accelerator(s) that may be attached to the machine as per accelerator_count. |
`accelerator_count` |
`int`
The number of accelerators to attach to the machine. |
`gpu_partition_size` |
`str`
Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to `Nvidia GPU Partitioning |
`tpu_topology` |
`str`
Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1"). |
`reservation_affinity` |
Optional. Immutable. Configuration controlling how this resource pool consumes reservation. |

## Methods

### MachineSpec

`MachineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a single machine.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreadtensorboardusageresponse_googlecloudaipla_4134e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardusageresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse -->

# Class ReadTensorboardUsageResponse (1.134.0)

```
ReadTensorboardUsageResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardUsage.

## Attribute |
|
|---|---|
Name |
Description |
`monthly_usage_data` |
`MutableMapping[str, `
Maps year-month (YYYYMM) string to per month usage data. |

## Classes

### MonthlyUsageDataEntry

`MonthlyUsageDataEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### PerMonthUsageData

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

### PerUserUsageData

`PerUserUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per user usage data.

## Methods

### ReadTensorboardUsageResponse

```
ReadTensorboardUsageResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardUsage.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoactionrecognitioninputsmodeltype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which c annot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_JETSON_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) to a Jetson device afterwards.

MOBILE_CORAL_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a Coral device afterwards.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestensorboard__googlecloudaiplatformv1beta1schematra_53131b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensorboard.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensorboard -->

# Class Tensorboard (1.134.0)

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the Tensorboard. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`display_name` |
`str`
Required. User provided name of this Tensorboard. |
`description` |
`str`
Description of this Tensorboard. |
`encryption_spec` |
Customer-managed encryption key spec for a Tensorboard. If set, this Tensorboard and all sub-resources of this Tensorboard will be secured by this key. |
`blob_storage_path_prefix` |
`str`
Output only. Consumer project Cloud Storage path prefix used to store blob data, which can either be a bucket or directory. Does not end with a '/'. |
`run_count` |
`int`
Output only. The number of Runs stored in this Tensorboard. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`is_default` |
`bool`
Used to indicate if the TensorBoard instance is the default one. Each project & region can have at most one default TensorBoard instance. Creation of a default TensorBoard instance and updating an existing TensorBoard instance to be default will mark all other TensorBoard instances (if any) as non default. |
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

### Tensorboard

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideo_8fd20c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideoactionrecognitioninputsmodeltype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognitionInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which c annot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_JETSON_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) to a Jetson device afterwards.

MOBILE_CORAL_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a Coral device afterwards.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesvertexaisearchdatastorespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexAISearch.DataStoreSpec -->

# Class DataStoreSpec (1.134.0)

`DataStoreSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Define data stores within engine to filter on in a search
call and configurations for those data stores. For more
information, see
[https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec](https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec)

## Attributes |
|
|---|---|
Name |
Description |
`data_store` |
`str`
Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`
|
`filter` |
`str`
Optional. Filter specification to filter documents in the data store specified by data_store field. For more information on filtering, see `Filtering ` __
|

## Methods

### DataStoreSpec

`DataStoreSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Define data stores within engine to filter on in a search
call and configurations for those data stores. For more
information, see
[https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec](https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessummarizationhelpfulnessinstance__googleclo_783e71.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessummarizationhelpfulnessinstance__googleclou_23c491.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessummarizationhelpfulnessinstance__googlecloud_3302e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessummarizationhelpfulnessinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessInstance -->

# Class SummarizationHelpfulnessInstance (1.134.0)

```
SummarizationHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to be summarized. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Optional. Summarization prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### SummarizationHelpfulnessInstance

```
SummarizationHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelcalltoactionopennotebooks_googl_237f2f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactionopennotebooks.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.OpenNotebooks -->

# Class OpenNotebooks (1.134.0)

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.

## Attribute |
|
|---|---|
Name |
Description |
`notebooks` |
`MutableSequence[`
Required. Regional resource references to notebooks. |

## Methods

### OpenNotebooks

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbleuinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BleuInput -->

# Class BleuInput (1.134.0)

`BleuInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for bleu metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for bleu score metric. |
`instances` |
`MutableSequence[`
Required. Repeated bleu instances. |

## Methods

### BleuInput

`BleuInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for bleu metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboard.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensorboard -->

# Class Tensorboard (1.134.0)

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the Tensorboard. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`display_name` |
`str`
Required. User provided name of this Tensorboard. |
`description` |
`str`
Description of this Tensorboard. |
`encryption_spec` |
Customer-managed encryption key spec for a Tensorboard. If set, this Tensorboard and all sub-resources of this Tensorboard will be secured by this key. |
`blob_storage_path_prefix` |
`str`
Output only. Consumer project Cloud Storage path prefix used to store blob data, which can either be a bucket or directory. Does not end with a '/'. |
`run_count` |
`int`
Output only. The number of Runs stored in this Tensorboard. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`is_default` |
`bool`
Used to indicate if the TensorBoard instance is the default one. Each project & region can have at most one default TensorBoard instance. Creation of a default TensorBoard instance and updating an existing TensorBoard instance to be default will mark all other TensorBoard instances (if any) as non default. |
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

### Tensorboard

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesexportfeaturevaluesresponse_googlecloudaipl_ae7894.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexportfeaturevaluesresponse_googlecloudaipla_af1146.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexportfeaturevaluesresponse_googlecloudaiplat_14671a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesResponse -->

# Class ExportFeatureValuesResponse (1.134.0)

`ExportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ExportFeatureValues.

## Methods

### ExportFeatureValuesResponse

`ExportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ExportFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesraymetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RayMetricSpec -->

# Class RayMetricSpec (1.134.0)

`RayMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray metrics.

## Attribute |
|
|---|---|
Name |
Description |
`disabled` |
`bool`
Optional. Flag to disable the Ray metrics collection. |

## Methods

### RayMetricSpec

`RayMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the Ray metrics.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelevaluationbiasconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluation.BiasConfig -->

# Class BiasConfig (1.134.0)

`BiasConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for bias detection.

## Attributes |
|
|---|---|
Name |
Description |
`bias_slices` |
Specification for how the data should be sliced for bias. It contains a list of slices, with limitation of two slices. The first slice of data will be the slice_a. The second slice in the list (slice_b) will be compared against the first slice. If only a single slice is provided, then slice_a will be compared against "not slice_a". Below are examples with feature "education" with value "low", "medium", "high" in the dataset: Example 1: :: bias_slices = [{'education': 'low'}] A single slice provided. In this case, slice_a is the collection of data with 'education' equals 'low', and slice_b is the collection of data with 'education' equals 'medium' or 'high'. Example 2: :: bias_slices = [{'education': 'low'}, {'education': 'high'}] Two slices provided. In this case, slice_a is the collection of data with 'education' equals 'low', and slice_b is the collection of data with 'education' equals 'high'. |
`labels` |
`MutableSequence[str]`
Positive labels selection on the target field. |

## Methods

### BiasConfig

`BiasConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for bias detection.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinefailurepolicy_googlecloudaiplatform_v_ed9e35.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinefailurepolicy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineFailurePolicy -->

# Class PipelineFailurePolicy (1.134.0)

`PipelineFailurePolicy(value)`


Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.

## Enums |
|
|---|---|
Name |
Description |
`PIPELINE_FAILURE_POLICY_UNSPECIFIED` |
Default value, and follows fail slow behavior. |
`PIPELINE_FAILURE_POLICY_FAIL_SLOW` |
Indicates that the pipeline should continue to run until all possible tasks have been scheduled and completed. |
`PIPELINE_FAILURE_POLICY_FAIL_FAST` |
Indicates that the pipeline should stop scheduling new tasks after a task has failed. |

## Methods

### PipelineFailurePolicy

`PipelineFailurePolicy(value)`


Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabelingdatasetconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig -->

# Class MigrateDataLabelingDatasetConfig (1.134.0)

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Required. Full resource name of data labeling Dataset. Format: `projects/{project}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
Optional. Display name of the Dataset in Vertex AI. System will pick a display name if unspecified. |
`migrate_data_labeling_annotated_dataset_configs` |
`MutableSequence[`
Optional. Configs for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery. The specified AnnotatedDatasets have to belong to the datalabeling Dataset. |

## Classes

### MigrateDataLabelingAnnotatedDatasetConfig

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.

## Methods

### MigrateDataLabelingDatasetConfig

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.
