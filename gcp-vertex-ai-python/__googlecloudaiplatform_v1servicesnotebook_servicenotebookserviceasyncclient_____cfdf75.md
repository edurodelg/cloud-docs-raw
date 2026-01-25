---
merged_at: 2026-01-25T21:47:44.353358
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesnotebook_servicenotebookserviceasyncclient______fc5d65.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicenotebookserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient -->

# Class NotebookServiceAsyncClient (1.134.0)

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

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
`NotebookServiceTransport` |
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

### NotebookServiceAsyncClient

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,NotebookServiceTransport,Callable[..., NotebookServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### assign_notebook_runtime

```
assign_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.AssignNotebookRuntimeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[str] = None,
notebook_runtime: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntime
] = None,
notebook_runtime_id: typing.Optional[str] = None,
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


Assigns a NotebookRuntime to a user for a particular Notebook file. This method will either returns an existing assignment or generates a new one.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime = aiplatform_v1.[NotebookRuntime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime.html)()
notebook_runtime.runtime_user = "runtime_user_value"
notebook_runtime.display_name = "display_name_value"
request = aiplatform_v1.[AssignNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeRequest.html)(
parent="parent_value",
notebook_runtime_template="notebook_runtime_template_value",
notebook_runtime=notebook_runtime,
)
# Make the request
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
Optional. User specified ID for the notebook runtime. This corresponds to the |
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

### create_notebook_execution_job

```
create_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.CreateNotebookExecutionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_execution_job: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_execution_job.NotebookExecutionJob
] = None,
notebook_execution_job_id: typing.Optional[str] = None,
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


Creates a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_execution_job = aiplatform_v1.[NotebookExecutionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.html)()
notebook_execution_job.notebook_runtime_template_resource_name = "notebook_runtime_template_resource_name_value"
notebook_execution_job.gcs_output_uri = "gcs_output_uri_value"
notebook_execution_job.execution_user = "execution_user_value"
request = aiplatform_v1.[CreateNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookExecutionJobRequest.html)(
parent="parent_value",
notebook_execution_job=notebook_execution_job,
)
# Make the request
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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

### create_notebook_runtime_template

```
create_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.CreateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
] = None,
notebook_runtime_template_id: typing.Optional[str] = None,
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


Creates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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

### delete_notebook_execution_job

```
delete_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.DeleteNotebookExecutionJobRequest,
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


Deletes a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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

### delete_notebook_runtime

```
delete_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.DeleteNotebookRuntimeRequest,
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


Deletes a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### delete_notebook_runtime_template

```
delete_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.DeleteNotebookRuntimeTemplateRequest,
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


Deletes a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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

### get_notebook_execution_job

```
get_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.GetNotebookExecutionJobRequest,
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
) -> google.cloud.aiplatform_v1.types.notebook_execution_job.NotebookExecutionJob
```


Gets a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
NotebookExecutionJob represents an instance of a notebook execution. |

### get_notebook_runtime

```
get_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.GetNotebookRuntimeRequest,
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
) -> google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntime
```


Gets a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade. |

### get_notebook_runtime_template

```
get_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.GetNotebookRuntimeTemplateRequest,
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
) -> google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
```


Gets a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

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
google.cloud.aiplatform_v1.services.notebook_service.transports.base.NotebookServiceTransport
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

### list_notebook_execution_jobs

```
list_notebook_execution_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
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
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager
)
```


Lists NotebookExecutionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
Response message for [NotebookService.CreateNotebookExecutionJob] Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtime_templates

```
list_notebook_runtime_templates(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
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
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager
)
```


Lists NotebookRuntimeTemplates in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
Response message for NotebookService.ListNotebookRuntimeTemplates. Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtimes

```
list_notebook_runtimes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
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
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager
)
```


Lists NotebookRuntimes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
Response message for NotebookService.ListNotebookRuntimes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_path

`notebook_runtime_path(project: str, location: str, notebook_runtime: str) -> str`


Returns a fully-qualified notebook_runtime string.

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

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

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_path

`parse_notebook_runtime_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

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

### start_notebook_runtime

```
start_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.StartNotebookRuntimeRequest,
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


Starts a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### stop_notebook_runtime

```
stop_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.StopNotebookRuntimeRequest,
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


Stops a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_notebook_runtime_template

```
update_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.UpdateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
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
) -> google.cloud.aiplatform_v1.types.notebook_runtime.NotebookRuntimeTemplate
```


Updates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = await client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. For the |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

### upgrade_notebook_runtime

```
upgrade_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.notebook_service.UpgradeNotebookRuntimeRequest,
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


Upgrades a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceAsyncClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typespublishermodelview_googlecloudaiplatform_2bbdb9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typespublishermodelview_googlecloudaiplatform__8769d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typespublishermodelview_googlecloudaiplatform_v_54ba51.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespublishermodelview_googlecloudaiplatform_v1_cf54b0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespublishermodelview_googlecloudaiplatform_v1b_316a2d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelview_googlecloudaiplatform_v1be_75f38a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelView -->

# Class PublisherModelView (1.134.0)

`PublisherModelView(value)`


View enumeration of PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`PUBLISHER_MODEL_VIEW_UNSPECIFIED` |
The default / unset value. The API will default to the BASIC view. |
`PUBLISHER_MODEL_VIEW_BASIC` |
Include basic metadata about the publisher model, but not the full contents. |
`PUBLISHER_MODEL_VIEW_FULL` |
Include everything. |
`PUBLISHER_MODEL_VERSION_VIEW_BASIC` |
Include: VersionId, ModelVersionExternalName, and SupportedActions. |

## Methods

### PublisherModelView

`PublisherModelView(value)`


View enumeration of PublisherModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployedmodelstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.Status -->

# Class Status (1.134.0)

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

## Attributes |
|
|---|---|
Name |
Description |
`message` |
`str`
Output only. The latest deployed model's status message (if any). |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The time at which the status was last updated. |
`available_replica_count` |
`int`
Output only. The number of available replicas of the deployed model. |

## Methods

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescodeexecutionresultoutcome_googlecloudaiplatf_9f38fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescodeexecutionresultoutcome.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CodeExecutionResult.Outcome -->

# Class Outcome (1.134.0)

`Outcome(value)`


Enumeration of possible outcomes of the code execution.

## Enums |
|
|---|---|
Name |
Description |
`OUTCOME_UNSPECIFIED` |
Unspecified status. This value should not be used. |
`OUTCOME_OK` |
Code execution completed successfully. |
`OUTCOME_FAILED` |
Code execution finished but with a failure. `stderr` should contain the reason. |
`OUTCOME_DEADLINE_EXCEEDED` |
Code execution ran for too long, and was cancelled. There may or may not be a partial output present. |

## Methods

### Outcome

`Outcome(value)`


Enumeration of possible outcomes of the code execution.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesliststudiesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse -->

# Class ListStudiesResponse (1.134.0)

`ListStudiesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`studies` |
`MutableSequence[`
The studies associated with the project. |
`next_page_token` |
`str`
Passes this token as the `page_token` field of the request
for a subsequent call. If this field is omitted, there are
no subsequent pages.
|

## Methods

### ListStudiesResponse

`ListStudiesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListStudies.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistfeatureviewsyncsrequest_googlecloudaiplatformv_fc1dd2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeatureviewsyncsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsRequest -->

# Class ListFeatureViewSyncsRequest (1.134.0)

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`filter` |
`str`
Lists the FeatureViewSyncs that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\"` -->
FeatureViewSyncs created after
2020-01-31T15:30:00.000000Z.
|
`page_size` |
`int`
The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViewSyncs call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViewSyncs must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
|

## Methods

### ListFeatureViewSyncsRequest

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformationcategoricaltransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.134.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgenerationconfig___googlecloudaiplatform_v1beta1ty_8eaa95.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgenerationconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig -->

# Class GenerationConfig (1.134.0)

`GenerationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Generation config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`temperature` |
`float`
Optional. Controls the randomness of predictions. This field is a member of `oneof` _ `_temperature` .
|
`top_p` |
`float`
Optional. If specified, nucleus sampling will be used. This field is a member of `oneof` _ `_top_p` .
|
`top_k` |
`float`
Optional. If specified, top-k sampling will be used. This field is a member of `oneof` _ `_top_k` .
|
`candidate_count` |
`int`
Optional. Number of candidates to generate. This field is a member of `oneof` _ `_candidate_count` .
|
`max_output_tokens` |
`int`
Optional. The maximum number of output tokens to generate per message. This field is a member of `oneof` _ `_max_output_tokens` .
|
`stop_sequences` |
`MutableSequence[str]`
Optional. Stop sequences. |
`response_logprobs` |
`bool`
Optional. If true, export the logprobs results in response. This field is a member of `oneof` _ `_response_logprobs` .
|
`logprobs` |
`int`
Optional. Logit probabilities. This field is a member of `oneof` _ `_logprobs` .
|
`presence_penalty` |
`float`
Optional. Positive penalties. This field is a member of `oneof` _ `_presence_penalty` .
|
`frequency_penalty` |
`float`
Optional. Frequency penalties. This field is a member of `oneof` _ `_frequency_penalty` .
|
`seed` |
`int`
Optional. Seed. This field is a member of `oneof` _ `_seed` .
|
`response_mime_type` |
`str`
Optional. Output response mimetype of the generated candidate text. Supported mimetype: - `text/plain` : (default) Text output.
- `application/json` : JSON response in the candidates. The
model needs to be prompted to output the appropriate
response type, otherwise the behavior is undefined. This
is a preview feature.
|
`response_schema` |
Optional. The `Schema` object allows the definition of
input and output data types. These types can be objects, but
also primitives and arrays. Represents a select subset of an
`OpenAPI 3.0 schema
object |
`response_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Output schema of the generated response. This is an alternative to `response_schema` that accepts `JSON
Schema |
`routing_config` |
Optional. Routing configuration. This field is a member of `oneof` _ `_routing_config` .
|
`speech_config` |
Optional. The speech generation config. This field is a member of `oneof` _ `_speech_config` .
|
`thinking_config` |
Optional. Config for thinking features. An error will be returned if this field is set for models that don't support thinking. |
`image_config` |
Optional. Config for image generation features. This field is a member of `oneof` _ `_image_config` .
|

## Classes

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ThinkingConfig

`ThinkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for thinking features.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### GenerationConfig

`GenerationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Generation config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespairwisesummarizationqualityinput_googleclou_a67778.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespairwisesummarizationqualityinput_googlecloud_b17654.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespairwisesummarizationqualityinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityInput -->

# Class PairwiseSummarizationQualityInput (1.134.0)

```
PairwiseSummarizationQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise summarization quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise summarization quality score metric. |
`instance` |
Required. Pairwise summarization quality instance. |

## Methods

### PairwiseSummarizationQualityInput

```
PairwiseSummarizationQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise summarization quality metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessInput -->

# Class QuestionAnsweringCorrectnessInput (1.134.0)

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering correctness score metric. |
`instance` |
Required. Question answering correctness instance. |

## Methods

### QuestionAnsweringCorrectnessInput

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatedatalabelingjobrequest_googlecloudaiplatform_7335ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatedatalabelingjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDataLabelingJobRequest -->

# Class CreateDataLabelingJobRequest (1.134.0)

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`data_labeling_job` |
Required. The DataLabelingJob to create. |

## Methods

### CreateDataLabelingJobRequest

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescomputetokensresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensResponse -->

# Class ComputeTokensResponse (1.134.0)

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.

## Attribute |
|
|---|---|
Name |
Description |
`tokens_info` |
`MutableSequence[`
Lists of tokens info from the input. A ComputeTokensRequest could have multiple instances with a prompt in each instance. We also need to return lists of tokens info for the request with multiple instances. |

## Methods

### ComputeTokensResponse

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.


---

<!-- DOCUMENTO FUSIONADO: _params_v1____googlecloudaiplatform_v1typespublishermodelview_googlecloudaiplatf_17c884.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: params_v1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/params_v1 -->

# Types for Google Cloud Aiplatform V1 Schema Predict Params v1 API

*class* google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageClassificationPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Image Classification.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageObjectDetectionPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Image Object Detection.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata’s predictionsLimit. Default value is 10.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageSegmentationPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Image Segmentation.

#### confidence_threshold()

When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoActionRecognitionPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Video Action Recognition.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoClassificationPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Video Classification.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000.

**Type**

#### segment_classification()

Set to true to request segment-level classification. Vertex AI returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true

**Type**

#### shot_classification()

Set to true to request shot-level classification. Vertex AI determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Vertex AI then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

**Type**

#### one_sec_interval_classification()

Set to true to request classification for a video at one-second intervals. Vertex AI returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### one_sec_interval_classification(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### segment_classification(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### shot_classification(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoObjectTrackingPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Video Object Tracking.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

**Type**

#### min_bounding_box_size()

Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### min_bounding_box_size(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typespublishermodelview_googlecloudaiplatform_v1beta1_0d516e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespublishermodelview_googlecloudaiplatform_v1beta1t_73ff88.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelview_googlecloudaiplatform_v1beta1ty_bae305.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModelView -->

# Class PublisherModelView (1.134.0)

`PublisherModelView(value)`


View enumeration of PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`PUBLISHER_MODEL_VIEW_UNSPECIFIED` |
The default / unset value. The API will default to the BASIC view. |
`PUBLISHER_MODEL_VIEW_BASIC` |
Include basic metadata about the publisher model, but not the full contents. |
`PUBLISHER_MODEL_VIEW_FULL` |
Include everything. |
`PUBLISHER_MODEL_VERSION_VIEW_BASIC` |
Include: VersionId, ModelVersionExternalName, and SupportedActions. |

## Methods

### PublisherModelView

`PublisherModelView(value)`


View enumeration of PublisherModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateexplanationdatasetoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetOperationMetadata -->

# Class UpdateExplanationDatasetOperationMetadata (1.134.0)

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateExplanationDatasetOperationMetadata

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1typesvideoobjecttrackingpredictionresultframe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult.Frame -->

# Class Frame (1.134.0)

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

## Attributes |
|
|---|---|
Name |
Description |
`time_offset` |
`google.protobuf.duration_pb2.Duration`
A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`x_min` |
`google.protobuf.wrappers_pb2.FloatValue`
The leftmost coordinate of the bounding box. |
`x_max` |
`google.protobuf.wrappers_pb2.FloatValue`
The rightmost coordinate of the bounding box. |
`y_min` |
`google.protobuf.wrappers_pb2.FloatValue`
The topmost coordinate of the bounding box. |
`y_max` |
`google.protobuf.wrappers_pb2.FloatValue`
The bottommost coordinate of the bounding box. |

## Methods

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesquestionansweringhelpfulnessinput_googleclou_a44077.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquestionansweringhelpfulnessinput_googlecloud_2c61e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringhelpfulnessinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessInput -->

# Class QuestionAnsweringHelpfulnessInput (1.134.0)

```
QuestionAnsweringHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering helpfulness score metric. |
`instance` |
Required. Question answering helpfulness instance. |

## Methods

### QuestionAnsweringHelpfulnessInput

```
QuestionAnsweringHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering helpfulness metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateexplanationdatasetoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetOperationMetadata -->

# Class UpdateExplanationDatasetOperationMetadata (1.134.0)

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateExplanationDatasetOperationMetadata

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistpipelinejobsresponse_googlecloudaiplatform_v1b_aac53c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistpipelinejobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse -->

# Class ListPipelineJobsResponse (1.134.0)

`ListPipelineJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PipelineService.ListPipelineJobs

## Attributes |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
List of PipelineJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListPipelineJobsRequest.page_token to obtain that page. |

## Methods

### ListPipelineJobsResponse

`ListPipelineJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PipelineService.ListPipelineJobs


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelarmorconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelArmorConfig -->

# Class ModelArmorConfig (1.134.0)

`ModelArmorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Model Armor integrations of prompt and responses.

## Attributes |
|
|---|---|
Name |
Description |
`prompt_template_name` |
`str`
Optional. The name of the Model Armor template to use for prompt sanitization. |
`response_template_name` |
`str`
Optional. The name of the Model Armor template to use for response sanitization. |

## Methods

### ModelArmorConfig

`ModelArmorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Model Armor integrations of prompt and responses.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesquestionansweringqualityspec_googleclouda_ef6cd7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesquestionansweringqualityspec_googlecloudai_7ccc86.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesquestionansweringqualityspec_googlecloudaip_a44ae0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesquestionansweringqualityspec_googlecloudaipl_264561.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquestionansweringqualityspec_googlecloudaipla_17445d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringqualityspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualitySpec -->

# Class QuestionAnsweringQualitySpec (1.134.0)

```
QuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality score metric.

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

### QuestionAnsweringQualitySpec

```
QuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality score metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescomputetokensresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ComputeTokensResponse -->

# Class ComputeTokensResponse (1.134.0)

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.

## Attribute |
|
|---|---|
Name |
Description |
`tokens_info` |
`MutableSequence[`
Lists of tokens info from the input. A ComputeTokensRequest could have multiple instances with a prompt in each instance. We also need to return lists of tokens info for the request with multiple instances. |

## Methods

### ComputeTokensResponse

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletedatasetversionrequest_googlecloudaiplatform__f1ac2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletedatasetversionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDatasetVersionRequest -->

# Class DeleteDatasetVersionRequest (1.134.0)

`DeleteDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|

## Methods

### DeleteDatasetVersionRequest

`DeleteDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDatasetVersion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewfeatureregistrysourcefeaturegroup.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.FeatureRegistrySource.FeatureGroup -->

# Class FeatureGroup (1.134.0)

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group_id` |
`str`
Required. Identifier of the feature group. |
`feature_ids` |
`MutableSequence[str]`
Required. Identifiers of features under the feature group. |

## Methods

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstoredcontentsexampleparameterscontentsearch_e0427d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstoredcontentsexampleparameterscontentsearchk_ddb457.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstoredcontentsexampleparameterscontentsearchkey.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleParameters.ContentSearchKey -->

# Class ContentSearchKey (1.134.0)

`ContentSearchKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The chat history to use to generate the search key for retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`contents` |
`MutableSequence[`
Required. The conversation for generating a search key. |
`search_key_generation_method` |
Required. The method of generating a search key. |

## Methods

### ContentSearchKey

`ContentSearchKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The chat history to use to generate the search key for retrieval.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexOperationMetadata -->

# Class DeployIndexOperationMetadata (1.134.0)

```
DeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.DeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployed_index_id` |
`str`
The unique index id specified by user |

## Methods

### DeployIndexOperationMetadata

```
DeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.DeployIndex.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesspeechconfig_googlecloudaiplatform_v1beta1typesfea_01b5e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesspeechconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeechConfig -->

# Class SpeechConfig (1.134.0)

`SpeechConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for speech generation.

## Attributes |
|
|---|---|
Name |
Description |
`voice_config` |
The configuration for the voice to use. |
`language_code` |
`str`
Optional. The language code (ISO 639-1) for the speech synthesis. |
`multi_speaker_voice_config` |
The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` .
|

## Methods

### SpeechConfig

`SpeechConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for speech generation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewfeatureregistrysourcefeaturegroup.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.FeatureRegistrySource.FeatureGroup -->

# Class FeatureGroup (1.134.0)

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group_id` |
`str`
Required. Identifier of the feature group. |
`feature_ids` |
`MutableSequence[str]`
Required. Identifiers of features under the feature group. |

## Methods

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessyncfeatureviewresponse_googlecloudaiplatfo_32f046.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessyncfeatureviewresponse_googlecloudaiplatfor_e57c0d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessyncfeatureviewresponse_googlecloudaiplatform_f67bd5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessyncfeatureviewresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SyncFeatureViewResponse -->

# Class SyncFeatureViewResponse (1.134.0)

`SyncFeatureViewResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.SyncFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`feature_view_sync` |
`str`
Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### SyncFeatureViewResponse

`SyncFeatureViewResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.SyncFeatureView.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesidmatcher.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IdMatcher -->

# Class IdMatcher (1.134.0)

`IdMatcher(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Matcher for Features of an EntityType by Feature ID.

## Attribute |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[str]`
Required. The following are accepted as `ids` :
- A single-element list containing only `*` , which selects
all Features in the target EntityType, or
- A list containing only Feature IDs, which selects only
Features with those IDs in the target EntityType.
|

## Methods

### IdMatcher

`IdMatcher(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Matcher for Features of an EntityType by Feature ID.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquestionansweringcorrectnessinput_googlecloudaipla_8e0195.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquestionansweringcorrectnessinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessInput -->

# Class QuestionAnsweringCorrectnessInput (1.134.0)

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering correctness score metric. |
`instance` |
Required. Question answering correctness instance. |

## Methods

### QuestionAnsweringCorrectnessInput

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessetpublishermodelconfigoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigOperationMetadata -->

# Class SetPublisherModelConfigOperationMetadata (1.134.0)

```
SetPublisherModelConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.SetPublisherModelConfig.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### SetPublisherModelConfigOperationMetadata

```
SetPublisherModelConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.SetPublisherModelConfig.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesspecialistpool__googlecloudaiplatform_v1typeslistn_07dccc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesspecialistpool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool -->

# Class SpecialistPool (1.134.0)

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool. |
`display_name` |
`str`
Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level. |
`specialist_managers_count` |
`int`
Output only. The number of managers in this SpecialistPool. |
`specialist_manager_emails` |
`MutableSequence[str]`
The email addresses of the managers in the SpecialistPool. |
`pending_data_labeling_jobs` |
`MutableSequence[str]`
Output only. The resource name of the pending data labeling jobs. |
`specialist_worker_emails` |
`MutableSequence[str]`
The email addresses of workers in the SpecialistPool. |

## Methods

### SpecialistPool

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistnasjobsresponse_googlecloudaiplatform_v1beta1t_4f8e34.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnasjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse -->

# Class ListNasJobsResponse (1.134.0)

`ListNasJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasJobs

## Attributes |
|
|---|---|
Name |
Description |
`nas_jobs` |
`MutableSequence[`
List of NasJobs in the requested page. NasJob.nas_job_output of the jobs will not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListNasJobsRequest.page_token to obtain that page. |

## Methods

### ListNasJobsResponse

`ListNasJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasJobs


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatedeploymentresourcepooloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolOperationMetadata -->

# Class UpdateDeploymentResourcePoolOperationMetadata (1.134.0)

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateDeploymentResourcePoolOperationMetadata

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typessearchdataitemsresponse_googlecloudaiplatf_51fb7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessearchdataitemsresponse_googlecloudaiplatfo_bb5480.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessearchdataitemsresponse_googlecloudaiplatfor_24e8a7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchdataitemsresponse_googlecloudaiplatform_149071.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchdataitemsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse -->

# Class SearchDataItemsResponse (1.134.0)

`SearchDataItemsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.SearchDataItems.

## Attributes |
|
|---|---|
Name |
Description |
`data_item_views` |
`MutableSequence[`
The DataItemViews read. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to SearchDataItemsRequest.page_token to obtain that page. |

## Methods

### SearchDataItemsResponse

`SearchDataItemsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.SearchDataItems.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfieldmappingrestrict.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping.Restrict -->

# Class Restrict (1.134.0)

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.

## Attributes |
|
|---|---|
Name |
Description |
`namespace` |
`str`
Required. The namespace of the restrict in the index. |
`allow_column` |
`MutableSequence[str]`
Optional. The columns containing the allow values. |
`deny_column` |
`MutableSequence[str]`
Optional. The columns containing the deny values. |

## Methods

### Restrict

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetadataschemametadataschematype_googleclouda_5a5982.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetadataschemametadataschematype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataSchema.MetadataSchemaType -->

# Class MetadataSchemaType (1.134.0)

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

## Enums |
|
|---|---|
Name |
Description |
`METADATA_SCHEMA_TYPE_UNSPECIFIED` |
Unspecified type for the MetadataSchema. |
`ARTIFACT_TYPE` |
A type indicating that the MetadataSchema will be used by Artifacts. |
`EXECUTION_TYPE` |
A typee indicating that the MetadataSchema will be used by Executions. |
`CONTEXT_TYPE` |
A state indicating that the MetadataSchema will be used by Contexts. |

## Methods

### MetadataSchemaType

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttuningjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse -->

# Class ListTuningJobsResponse (1.134.0)

`ListTuningJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for GenAiTuningService.ListTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`tuning_jobs` |
`MutableSequence[`
List of TuningJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListTuningJobsResponse

`ListTuningJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for GenAiTuningService.ListTuningJobs


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforec_0455cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastinginputstransformationcategoricaltransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.134.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeatureviewsyncsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsRequest -->

# Class ListFeatureViewSyncsRequest (1.134.0)

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`filter` |
`str`
Lists the FeatureViewSyncs that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\"` -->
FeatureViewSyncs created after
2020-01-31T15:30:00.000000Z.
|
`page_size` |
`int`
The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViewSyncs call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViewSyncs must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
|

## Methods

### ListFeatureViewSyncsRequest

`ListFeatureViewSyncsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespointwisemetricinstance__googlecloudaiplatfo_fb7222.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespointwisemetricinstance__googlecloudaiplatfor_44cbd8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespointwisemetricinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricInstance -->

# Class PointwiseMetricInstance (1.134.0)

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

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
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PointwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|
`content_map_instance` |
Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. This field is a member of `oneof` _ `instance` .
|

## Methods

### PointwiseMetricInstance

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescancelbatchpredictionjobrequest_googlecloudai_ce3b3f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescancelbatchpredictionjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelBatchPredictionJobRequest -->

# Class CancelBatchPredictionJobRequest (1.134.0)

```
CancelBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob to cancel. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### CancelBatchPredictionJobRequest

```
CancelBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelBatchPredictionJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataRequest -->

# Class ImportDataRequest (1.134.0)

`ImportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ImportData.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`import_configs` |
`MutableSequence[`
Required. The desired input locations. The contents of all input locations will be imported in one batch. |

## Methods

### ImportDataRequest

`ImportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ImportData.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesspecialistpool_googlecloudaiplatformv1beta1sc_c21bb0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesspecialistpool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool -->

# Class SpecialistPool (1.134.0)

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SpecialistPool. |
`display_name` |
`str`
Required. The user-defined name of the SpecialistPool. The name can be up to 128 characters long and can consist of any UTF-8 characters. This field should be unique on project-level. |
`specialist_managers_count` |
`int`
Output only. The number of managers in this SpecialistPool. |
`specialist_manager_emails` |
`MutableSequence[str]`
The email addresses of the managers in the SpecialistPool. |
`pending_data_labeling_jobs` |
`MutableSequence[str]`
Output only. The resource name of the pending data labeling jobs. |
`specialist_worker_emails` |
`MutableSequence[str]`
The email addresses of workers in the SpecialistPool. |

## Methods

### SpecialistPool

`SpecialistPool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlimageobjectdetectioninputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs -->

# Class AutoMlImageObjectDetectionInputs (1.134.0)

```
AutoMlImageObjectDetectionInputs(
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
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used. |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: ____params_v1beta1____googlecloudaiplatform_v1beta1typesspeculativedecodingspecd_bbbf4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___params_v1beta1____googlecloudaiplatform_v1beta1typesspeculativedecodingspecdr_b70bb8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __params_v1beta1____googlecloudaiplatform_v1beta1typesspeculativedecodingspecdra_4ca4bd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _params_v1beta1____googlecloudaiplatform_v1beta1typesspeculativedecodingspecdraf_91040a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: params_v1beta1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/params_v1beta1 -->

# Types for Google Cloud Aiplatform V1beta1 Schema Predict Params v1beta1 API

*class* google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageClassificationPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Image Classification.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageObjectDetectionPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Image Object Detection.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata’s predictionsLimit. Default value is 10.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageSegmentationPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Image Segmentation.

#### confidence_threshold()

When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoActionRecognitionPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Video Action Recognition.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoClassificationPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Video Classification.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000.

**Type**

#### segment_classification()

Set to true to request segment-level classification. Vertex AI returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true

**Type**

#### shot_classification()

Set to true to request shot-level classification. Vertex AI determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Vertex AI then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

**Type**

#### one_sec_interval_classification()

Set to true to request classification for a video at one-second intervals. Vertex AI returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### one_sec_interval_classification(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### segment_classification(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### shot_classification(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoObjectTrackingPredictionParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction model parameters for Video Object Tracking.

#### confidence_threshold()

The Model only returns predictions with at least this confidence score. Default value is 0.0

**Type**

#### max_predictions()

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

**Type**

#### min_bounding_box_size()

Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0.

**Type**

#### confidence_threshold(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### max_predictions(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### min_bounding_box_size(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesspeculativedecodingspecdraftmodelspeculatio_a62ae1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesspeculativedecodingspecdraftmodelspeculation_c977cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesspeculativedecodingspecdraftmodelspeculation__6251c2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesspeculativedecodingspecdraftmodelspeculation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeculativeDecodingSpec.DraftModelSpeculation -->

# Class DraftModelSpeculation (1.134.0)

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

## Attribute |
|
|---|---|
Name |
Description |
`draft_model` |
`str`
Required. The resource name of the draft model. |

## Methods

### DraftModelSpeculation

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletedatalabelingjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDataLabelingJobRequest -->

# Class DeleteDataLabelingJobRequest (1.134.0)

```
DeleteDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteDataLabelingJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DataLabelingJob to be deleted. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
|

## Methods

### DeleteDataLabelingJobRequest

```
DeleteDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteDataLabelingJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationcategoricaltransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation -->

# Class CategoricalTransformation (1.134.0)

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

## Methods

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeploymodelrequest__googlecloudaiplatform_v1beta1t_7a63e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeploymodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest -->

# Class DeployModelRequest (1.134.0)

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. |

## Classes

### TrafficSplitEntry

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DeployModelRequest

`DeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeployModel.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbatchcancelpipelinejobsoperationmetadata_goog_2a5755.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchcancelpipelinejobsoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsOperationMetadata -->

# Class BatchCancelPipelineJobsOperationMetadata (1.134.0)

```
BatchCancelPipelineJobsOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for PipelineService.BatchCancelPipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### BatchCancelPipelineJobsOperationMetadata

```
BatchCancelPipelineJobsOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for PipelineService.BatchCancelPipelineJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecparameterspecconditionalparameterspecintvaluecondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.IntValueCondition -->

# Class IntValueCondition (1.134.0)

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[int]`
Required. Matches values of the parent parameter of 'INTEGER' type. All values must lie in `integer_value_spec` of parent parameter.
|

## Methods

### IntValueCondition

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typeslistspecialistpoolsresponse_googlecloudaiplatfo_19760e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistspecialistpoolsresponse_googlecloudaiplatfor_e10e0e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistspecialistpoolsresponse_googlecloudaiplatform_64a357.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistspecialistpoolsresponse_googlecloudaiplatform__a87079.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistspecialistpoolsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse -->

# Class ListSpecialistPoolsResponse (1.134.0)

`ListSpecialistPoolsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SpecialistPoolService.ListSpecialistPools.

## Attributes |
|
|---|---|
Name |
Description |
`specialist_pools` |
`MutableSequence[`
A list of SpecialistPools that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListSpecialistPoolsResponse

`ListSpecialistPoolsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SpecialistPoolService.ListSpecialistPools.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescanceltrainingpipelinerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest -->

# Class CancelTrainingPipelineRequest (1.134.0)

```
CancelTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CancelTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### CancelTrainingPipelineRequest

```
CancelTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CancelTrainingPipeline.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletetrainingpipelinerequest_googlecloudaiplatfor_be1cca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletetrainingpipelinerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrainingPipelineRequest -->

# Class DeleteTrainingPipelineRequest (1.134.0)

```
DeleteTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.DeleteTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### DeleteTrainingPipelineRequest

```
DeleteTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.DeleteTrainingPipeline.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessecretenvvar.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SecretEnvVar -->

# Class SecretEnvVar (1.134.0)

`SecretEnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable where the value is a secret in Cloud Secret Manager.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name of the secret environment variable. |
`secret_ref` |
Required. Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable. |

## Methods

### SecretEnvVar

`SecretEnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable where the value is a secret in Cloud Secret Manager.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexportdataconfig__googlecloudaiplatform_v1typ_7458bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportdataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig -->

# Class ExportDataConfig (1.134.0)

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_destination` |
The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: `export-data-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All export output will be written into that
directory. Inside that directory, annotations with the same
schema will be grouped into sub directories which are named
with the corresponding annotations' schema title. Inside
these sub directories, a schema.yaml will be created to
describe the output format.
This field is a member of `oneof` _ `destination` .
|
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`annotations_filter` |
`str`
An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in ListAnnotations. |

## Methods

### ExportDataConfig

`ExportDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes what part of the Dataset is to be exported, the destination of the export and how to export.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquestionansweringcorrectnessspec_googlecloudaiplat_65e1db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquestionansweringcorrectnessspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessSpec -->

# Class QuestionAnsweringCorrectnessSpec (1.134.0)

```
QuestionAnsweringCorrectnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering correctness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringCorrectnessSpec

```
QuestionAnsweringCorrectnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistpersistentresourcesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse -->

# Class ListPersistentResourcesResponse (1.134.0)

```
ListPersistentResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PersistentResourceService.ListPersistentResources

## Attribute |
|
|---|---|
Name |
Description |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListPersistentResourcesRequest.page_token to obtain that page. |

## Methods

### ListPersistentResourcesResponse

```
ListPersistentResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PersistentResourceService.ListPersistentResources


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesevent_googlecloudaiplatform_v1beta1typesevent___g_ee4bca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesevent_googlecloudaiplatform_v1beta1typesevent.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesevent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Event -->

# Class Event (1.134.0)

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An edge describing the relationship between an Artifact and an Execution in a lineage graph.

## Attributes |
|
|---|---|
Name |
Description |
`artifact` |
`str`
Required. The relative resource name of the Artifact in the Event. |
`execution` |
`str`
Output only. The relative resource name of the Execution in the Event. |
`event_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time the Event occurred. |
`type_` |
Required. The type of the Event. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to annotate Events. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Event (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |

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

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Methods

### Event

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An edge describing the relationship between an Artifact and an Execution in a lineage graph.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Event -->

# Class Event (1.134.0)

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An edge describing the relationship between an Artifact and an Execution in a lineage graph.

## Attributes |
|
|---|---|
Name |
Description |
`artifact` |
`str`
Required. The relative resource name of the Artifact in the Event. |
`execution` |
`str`
Output only. The relative resource name of the Execution in the Event. |
`event_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time the Event occurred. |
`type_` |
Required. The type of the Event. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to annotate Events. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Event (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |

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

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Methods

### Event

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An edge describing the relationship between an Artifact and an Execution in a lineage graph.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesquestionansweringhelpfulnessspec_googlecloudaipla_66c9fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquestionansweringhelpfulnessspec_googlecloudaiplat_841992.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquestionansweringhelpfulnessspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringHelpfulnessSpec -->

# Class QuestionAnsweringHelpfulnessSpec (1.134.0)

```
QuestionAnsweringHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering helpfulness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringHelpfulnessSpec

```
QuestionAnsweringHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesschedulestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.State -->

# Class State (1.134.0)

`State(value)`


Possible state of the schedule.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified. |
`ACTIVE` |
The Schedule is active. Runs are being scheduled on the user-specified timespec. |
`PAUSED` |
The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete. |
`COMPLETED` |
The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

## Methods

### State

`State(value)`


Possible state of the schedule.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimageobjectdetectioninputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs -->

# Class AutoMlImageObjectDetectionInputs (1.134.0)

```
AutoMlImageObjectDetectionInputs(
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
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used. |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageObjectDetectionInputs

```
AutoMlImageObjectDetectionInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeslistragcorporaresponse_googlecloudaiplatf_47d391.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistragcorporaresponse_googlecloudaiplatfo_38a12e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistragcorporaresponse_googlecloudaiplatfor_70537f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistragcorporaresponse_googlecloudaiplatform_88c3e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistragcorporaresponse_googlecloudaiplatform__d588a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistragcorporaresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse -->

# Class ListRagCorporaResponse (1.134.0)

`ListRagCorporaResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagCorpora.

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpora` |
`MutableSequence[`
List of RagCorpora in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListRagCorporaRequest.page_token to obtain that page. |

## Methods

### ListRagCorporaResponse

`ListRagCorporaResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagCorpora.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessafetysettingharmblockthreshold.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetySetting.HarmBlockThreshold -->

# Class HarmBlockThreshold (1.134.0)

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

## Enums |
|
|---|---|
Name |
Description |
`HARM_BLOCK_THRESHOLD_UNSPECIFIED` |
Unspecified harm block threshold. |
`BLOCK_LOW_AND_ABOVE` |
Block low threshold and above (i.e. block more). |
`BLOCK_MEDIUM_AND_ABOVE` |
Block medium threshold and above. |
`BLOCK_ONLY_HIGH` |
Block only high threshold (i.e. block less). |
`BLOCK_NONE` |
Block none. |
`OFF` |
Turn off the safety filter. |

## Methods

### HarmBlockThreshold

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatememoryrequest_googlecloudaiplatform_v1b_9a647d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatememoryrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryRequest -->

# Class CreateMemoryRequest (1.134.0)

`CreateMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.CreateMemory.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to create the Memory under. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`memory` |
Required. The Memory to be created. |

## Methods

### CreateMemoryRequest

`CreateMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.CreateMemory.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievecontextsrequestvertexragstoreragresource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.VertexRagStore.RagResource -->

# Class RagResource (1.134.0)

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpus` |
`str`
Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`rag_file_ids` |
`MutableSequence[str]`
Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field. |

## Methods

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreateindexendpointrequest_googlecloudaiplatform__f9a8f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreateindexendpointrequest_googlecloudaiplatform_v_b36222.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateindexendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexEndpointRequest -->

# Class CreateIndexEndpointRequest (1.134.0)

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: `projects/{project}/locations/{location}`
|
`index_endpoint` |
Required. The IndexEndpoint to create. |

## Methods

### CreateIndexEndpointRequest

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexOperationMetadata -->

# Class UpdateIndexOperationMetadata (1.134.0)

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### UpdateIndexOperationMetadata

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensor -->

# Class Tensor (1.134.0)

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.

## Attributes |
|
|---|---|
Name |
Description |
`dtype` |
The data type of tensor. |
`shape` |
`MutableSequence[int]`
Shape of the tensor. |
`bool_val` |
`MutableSequence[bool]`
Type specific representations that make it easy to create tensor protos in all languages. Only the representation corresponding to "dtype" can be set. The values hold the flattened representation of the tensor in row major order. BOOL |
`string_val` |
`MutableSequence[str]`
STRING |
`bytes_val` |
`MutableSequence[bytes]`
STRING |
`float_val` |
`MutableSequence[float]`
FLOAT |
`double_val` |
`MutableSequence[float]`
DOUBLE |
`int_val` |
`MutableSequence[int]`
INT_8 INT_16 INT_32 |
`int64_val` |
`MutableSequence[int]`
INT64 |
`uint_val` |
`MutableSequence[int]`
UINT8 UINT16 UINT32 |
`uint64_val` |
`MutableSequence[int]`
UINT64 |
`list_val` |
`MutableSequence[google.cloud.aiplatform_v1.types.Tensor]`
A list of tensor values. |
`struct_val` |
`MutableMapping[str, google.cloud.aiplatform_v1.types.Tensor]`
A map of string to tensor. |
`tensor_val` |
`bytes`
Serialized raw tensor content. |

## Classes

### DataType

`DataType(value)`


Data type of the tensor.

### StructValEntry

`StructValEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### Tensor

`Tensor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A tensor value type.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesfeature_online_store_service_googlecloudaipla_715a5c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeature_online_store_service_googlecloudaiplat_ed1df9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_online_store_service_googlecloudaiplatf_d39a00.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service -->

# Package feature_online_store_service (1.134.0)

API documentation for `aiplatform_v1.services.feature_online_store_service`

package.

## Classes

[FeatureOnlineStoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient)

A service for fetching feature values from the online store.

[FeatureOnlineStoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient)

A service for fetching feature values from the online store.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeatureviewrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureViewRequest -->

# Class DeleteFeatureViewRequest (1.134.0)

`DeleteFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.DeleteFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureView to be deleted. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### DeleteFeatureViewRequest

`DeleteFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.DeleteFeatureView.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatedatalabelingjobrequest_googlecloudaipla_903869.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatedatalabelingjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDataLabelingJobRequest -->

# Class CreateDataLabelingJobRequest (1.134.0)

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`data_labeling_job` |
Required. The DataLabelingJob to create. |

## Methods

### CreateDataLabelingJobRequest

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdatalabelingjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse -->

# Class ListDataLabelingJobsResponse (1.134.0)

```
ListDataLabelingJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`data_labeling_jobs` |
`MutableSequence[`
A list of DataLabelingJobs that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListDataLabelingJobsResponse

```
ListDataLabelingJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListDataLabelingJobs.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesquestionansweringrelevancespec_googlecloudai_2ce1b2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquestionansweringrelevancespec_googlecloudaip_49c261.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringrelevancespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceSpec -->

# Class QuestionAnsweringRelevanceSpec (1.134.0)

```
QuestionAnsweringRelevanceSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering relevance. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringRelevanceSpec

```
QuestionAnsweringRelevanceSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesremovedatapointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsRequest -->

# Class RemoveDatapointsRequest (1.134.0)

`RemoveDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.RemoveDatapoints

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`str`
Required. The name of the Index resource to be updated. Format: `projects/{project}/locations/{location}/indexes/{index}`
|
`datapoint_ids` |
`MutableSequence[str]`
A list of datapoint ids to be deleted. |

## Methods

### RemoveDatapointsRequest

`RemoveDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.RemoveDatapoints


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesvideoobjecttrackingpredictionresultframe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame -->

# Class Frame (1.134.0)

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

## Attributes |
|
|---|---|
Name |
Description |
`time_offset` |
`google.protobuf.duration_pb2.Duration`
A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`x_min` |
`google.protobuf.wrappers_pb2.FloatValue`
The leftmost coordinate of the bounding box. |
`x_max` |
`google.protobuf.wrappers_pb2.FloatValue`
The rightmost coordinate of the bounding box. |
`y_min` |
`google.protobuf.wrappers_pb2.FloatValue`
The topmost coordinate of the bounding box. |
`y_max` |
`google.protobuf.wrappers_pb2.FloatValue`
The bottommost coordinate of the bounding box. |

## Methods

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

### Frame

`Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesimportragfilesconfig___googlecloudaiplatform_v1ty_a5c2e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesimportragfilesconfig___googlecloudaiplatform_v1typ_d25fe4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportragfilesconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportRagFilesConfig -->

# Class ImportRagFilesConfig (1.134.0)

`ImportRagFilesConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for importing RagFiles.

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
`gcs_source` |
Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucket_name/my_directory/object_name/my_file.txt`
- `gs://bucket_name/my_directory`
This field is a member of `oneof` _ `import_source` .
|
`google_drive_source` |
Google Drive location. Supports importing individual files as well as Google Drive folders. This field is a member of `oneof` _ `import_source` .
|
`slack_source` |
Slack channels with their corresponding access tokens. This field is a member of `oneof` _ `import_source` .
|
`jira_source` |
Jira queries with their corresponding authentication. This field is a member of `oneof` _ `import_source` .
|
`share_point_sources` |
SharePoint sources. This field is a member of `oneof` _ `import_source` .
|
`partial_failure_gcs_sink` |
The Cloud Storage path to write partial failures to. Deprecated. Prefer to use `import_result_gcs_sink` .
This field is a member of `oneof` _ `partial_failure_sink` .
|
`partial_failure_bigquery_sink` |
The BigQuery destination to write partial failures to. It should be a bigquery table resource name (e.g. "bq://projectId.bqDatasetId.bqTableId"). The dataset must exist. If the table does not exist, it will be created with the expected schema. If the table exists, the schema will be validated and data will be added to this existing table. Deprecated. Prefer to use `import_result_bq_sink` .
This field is a member of `oneof` _ `partial_failure_sink` .
|
`import_result_gcs_sink` |
The Cloud Storage path to write import result to. This field is a member of `oneof` _ `import_result_sink` .
|
`import_result_bigquery_sink` |
The BigQuery destination to write import result to. It should be a bigquery table resource name (e.g. "bq://projectId.bqDatasetId.bqTableId"). The dataset must exist. If the table does not exist, it will be created with the expected schema. If the table exists, the schema will be validated and data will be added to this existing table. This field is a member of `oneof` _ `import_result_sink` .
|
`rag_file_transformation_config` |
Specifies the transformation config for RagFiles. |
`rag_file_parsing_config` |
Optional. Specifies the parsing config for RagFiles. RAG will use the default parser if this field is not set. |
`max_embedding_requests_per_min` |
`int`
Optional. The max number of queries per minute that this job is allowed to make to the embedding model specified on the corpus. This value is specific to this job and not shared across other import jobs. Consult the Quotas page on the project to set an appropriate value here. If unspecified, a default value of 1,000 QPM would be used. |
`rebuild_ann_index` |
`bool`
Rebuilds the ANN index to optimize for recall on the imported data. Only applicable for RagCorpora running on RagManagedDb with `retrieval_strategy` set to `ANN` . The
rebuild will be performed using the existing ANN config set
on the RagCorpus. To change the ANN config, please use the
UpdateRagCorpus API.
Default is false, i.e., index is not rebuilt.
|

## Methods

### ImportRagFilesConfig

`ImportRagFilesConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for importing RagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdatedeploymentresourcepooloperationmetadata_goo_60d593.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatedeploymentresourcepooloperationmetadata_goog_4ab878.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatedeploymentresourcepooloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDeploymentResourcePoolOperationMetadata -->

# Class UpdateDeploymentResourcePoolOperationMetadata (1.134.0)

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateDeploymentResourcePoolOperationMetadata

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatedeploymentresourcepooloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolOperationMetadata -->

# Class CreateDeploymentResourcePoolOperationMetadata (1.134.0)

```
CreateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for CreateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDeploymentResourcePoolOperationMetadata

```
CreateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for CreateDeploymentResourcePool method.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdateindexrequest_googlecloudaiplatform_v1beta1ty_f69cf0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexRequest -->

# Class UpdateIndexRequest (1.134.0)

`UpdateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
Required. The Index which updates the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexRequest

`UpdateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpdateIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewdirectwriteresponsewriteresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteResponse.WriteResponse -->

# Class WriteResponse (1.134.0)

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

## Attributes |
|
|---|---|
Name |
Description |
`data_key` |
What key is this write response associated with. |
`online_store_write_time` |
`google.protobuf.timestamp_pb2.Timestamp`
When the feature values were written to the online store. If FeatureViewDirectWriteResponse.status is not OK, this field is not populated. |

## Methods

### WriteResponse

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesdeletetensorboardrunrequest_googlecloudaipl_e0576b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeletetensorboardrunrequest_googlecloudaipla_380d69.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletetensorboardrunrequest_googlecloudaiplat_12bb5c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletetensorboardrunrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRunRequest -->

# Class DeleteTensorboardRunRequest (1.134.0)

`DeleteTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboardRun.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardRun to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### DeleteTensorboardRunRequest

`DeleteTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboardRun.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrestoredatasetversionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionRequest -->

# Class RestoreDatasetVersionRequest (1.134.0)

```
RestoreDatasetVersionRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DatasetService.RestoreDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DatasetVersion resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|

## Methods

### RestoreDatasetVersionRequest

```
RestoreDatasetVersionRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DatasetService.RestoreDatasetVersion.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistsessionsresponse_googlecloudaiplatform_v1_d380d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistsessionsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse -->

# Class ListSessionsResponse (1.134.0)

`ListSessionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListSessions.

## Attributes |
|
|---|---|
Name |
Description |
`sessions` |
`MutableSequence[`
A list of sessions matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListSessionsRequest.page_token to retrieve the next page. Absence of this field indicates there are no subsequent pages. |

## Methods

### ListSessionsResponse

`ListSessionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListSessions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesschedulestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.State -->

# Class State (1.134.0)

`State(value)`


Possible state of the schedule.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified. |
`ACTIVE` |
The Schedule is active. Runs are being scheduled on the user-specified timespec. |
`PAUSED` |
The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete. |
`COMPLETED` |
The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

## Methods

### State

`State(value)`


Possible state of the schedule.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreateindexoperationmetadata_googlecloudaiplatfor_e22cc6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreateindexoperationmetadata_googlecloudaiplatform_c970e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexOperationMetadata -->

# Class CreateIndexOperationMetadata (1.134.0)

```
CreateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.CreateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### CreateIndexOperationMetadata

```
CreateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.CreateIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexOperationMetadata -->

# Class UpdateIndexOperationMetadata (1.134.0)

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### UpdateIndexOperationMetadata

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreateindexendpointrequest__summary_method_su_d38a8a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateindexendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointRequest -->

# Class CreateIndexEndpointRequest (1.134.0)

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: `projects/{project}/locations/{location}`
|
`index_endpoint` |
Required. The IndexEndpoint to create. |

## Methods

### CreateIndexEndpointRequest

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.


---

<!-- DOCUMENTO FUSIONADO: _summary_method_summary_methodhtml.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: summary_method.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/summary_method -->

# aiplatform (1.134.0)

Documentation is too large to display. See the GitHub repository: https://github.com/googleapis/python-aiplatform


---

<!-- DOCUMENTO FUSIONADO: summary_methodhtml.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/summary_method.html -->

# aiplatform (1.134.0)

Documentation is too large to display. See the GitHub repository: https://github.com/googleapis/python-aiplatform


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_servicenotebookserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient -->

# Class NotebookServiceAsyncClient (1.134.0)

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

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
`NotebookServiceTransport` |
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

### NotebookServiceAsyncClient

```
NotebookServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,NotebookServiceTransport,Callable[..., NotebookServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### assign_notebook_runtime

```
assign_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.AssignNotebookRuntimeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[str] = None,
notebook_runtime: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntime
] = None,
notebook_runtime_id: typing.Optional[str] = None,
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


Assigns a NotebookRuntime to a user for a particular Notebook file. This method will either returns an existing assignment or generates a new one.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime = aiplatform_v1beta1.[NotebookRuntime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.html)()
notebook_runtime.runtime_user = "runtime_user_value"
notebook_runtime.display_name = "display_name_value"
request = aiplatform_v1beta1.[AssignNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest.html)(
parent="parent_value",
notebook_runtime_template="notebook_runtime_template_value",
notebook_runtime=notebook_runtime,
)
# Make the request
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
Optional. User specified ID for the notebook runtime. This corresponds to the |
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

### create_notebook_execution_job

```
create_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.CreateNotebookExecutionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_execution_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_execution_job.NotebookExecutionJob
] = None,
notebook_execution_job_id: typing.Optional[str] = None,
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


Creates a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_execution_job = aiplatform_v1beta1.[NotebookExecutionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.html)()
notebook_execution_job.notebook_runtime_template_resource_name = "notebook_runtime_template_resource_name_value"
notebook_execution_job.gcs_output_uri = "gcs_output_uri_value"
notebook_execution_job.execution_user = "execution_user_value"
request = aiplatform_v1beta1.[CreateNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobRequest.html)(
parent="parent_value",
notebook_execution_job=notebook_execution_job,
)
# Make the request
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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

### create_notebook_runtime_template

```
create_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.CreateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
] = None,
notebook_runtime_template_id: typing.Optional[str] = None,
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


Creates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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

### delete_notebook_execution_job

```
delete_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookExecutionJobRequest,
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


Deletes a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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

### delete_notebook_runtime

```
delete_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookRuntimeRequest,
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


Deletes a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### delete_notebook_runtime_template

```
delete_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.DeleteNotebookRuntimeTemplateRequest,
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


Deletes a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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
`NotebookServiceAsyncClient` |
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

### get_notebook_execution_job

```
get_notebook_execution_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookExecutionJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_execution_job.NotebookExecutionJob
```


Gets a NotebookExecutionJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
NotebookExecutionJob represents an instance of a notebook execution. |

### get_notebook_runtime

```
get_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookRuntimeRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntime
```


Gets a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade. |

### get_notebook_runtime_template

```
get_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.GetNotebookRuntimeTemplateRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
```


Gets a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

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
google.cloud.aiplatform_v1beta1.services.notebook_service.transports.base.NotebookServiceTransport
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

### list_notebook_execution_jobs

```
list_notebook_execution_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager
)
```


Lists NotebookExecutionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
Response message for [NotebookService.CreateNotebookExecutionJob] Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtime_templates

```
list_notebook_runtime_templates(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager
)
```


Lists NotebookRuntimeTemplates in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
Response message for NotebookService.ListNotebookRuntimeTemplates. Iterating over this object will yield results and resolve additional pages automatically. |

### list_notebook_runtimes

```
list_notebook_runtimes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
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
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager
)
```


Lists NotebookRuntimes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
Response message for NotebookService.ListNotebookRuntimes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_path

`notebook_runtime_path(project: str, location: str, notebook_runtime: str) -> str`


Returns a fully-qualified notebook_runtime string.

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

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

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_path

`parse_notebook_runtime_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

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

### start_notebook_runtime

```
start_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.StartNotebookRuntimeRequest,
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


Starts a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### stop_notebook_runtime

```
stop_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.StopNotebookRuntimeRequest,
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


Stops a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_notebook_runtime_template

```
update_notebook_runtime_template(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.UpdateNotebookRuntimeTemplateRequest,
dict,
]
] = None,
*,
notebook_runtime_template: typing.Optional[
google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
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
) -> google.cloud.aiplatform_v1beta1.types.notebook_runtime.NotebookRuntimeTemplate
```


Updates a NotebookRuntimeTemplate.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = await client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. For the |
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
A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template. |

### upgrade_notebook_runtime

```
upgrade_notebook_runtime(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.notebook_service.UpgradeNotebookRuntimeRequest,
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


Upgrades a NotebookRuntime.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceAsyncClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
