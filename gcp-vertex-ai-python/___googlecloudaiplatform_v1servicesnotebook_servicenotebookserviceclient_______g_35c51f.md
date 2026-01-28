---
merged_at: 2026-01-28T15:11:44.759043
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient -->

# Class NotebookServiceClient (1.135.0)

```
NotebookServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### NotebookServiceClient

```
NotebookServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
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
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
`str`
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
`str`
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
`str`
Optional. User specified ID for the notebook runtime. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
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
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
`str`
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
`str`
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceClient` |
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
`NotebookServiceClient` |
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
`NotebookServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
`str`
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookExecutionJobsPager
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
def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager
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
def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimesPager
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
def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1_services_notebook_service_NotebookServiceClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexDatapoint.CrowdingTag -->

# Class CrowdingTag (1.135.0)

`CrowdingTag(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute.

## Attribute |
|
|---|---|
Name |
Description |
`crowding_attribute` |
`str`
The attribute value used for crowding. The maximum number of neighbors to return per crowding attribute value (per_crowding_attribute_num_neighbors) is configured per-query. This field is ignored if per_crowding_attribute_num_neighbors is larger than the total number of neighbors to return for a given query. |

## Methods

### CrowdingTag

`CrowdingTag(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsRequest -->

# Class QueryDeployedModelsRequest (1.135.0)

`QueryDeployedModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for QueryDeployedModels method.

## Attributes |
|
|---|---|
Name |
Description |
`deployment_resource_pool` |
`str`
Required. The name of the target DeploymentResourcePool to query. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|
`page_size` |
`int`
The maximum number of DeployedModels to return. The service may return fewer than this value. |
`page_token` |
`str`
A page token, received from a previous `QueryDeployedModels` call. Provide this to retrieve the
subsequent page.
When paginating, all other parameters provided to
`QueryDeployedModels` must match the call that provided
the page token.
|

## Methods

### QueryDeployedModelsRequest

`QueryDeployedModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for QueryDeployedModels method.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceRequest -->

# Class CreatePersistentResourceRequest (1.135.0)

```
CreatePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.CreatePersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the PersistentResource in. Format: `projects/{project}/locations/{location}`
|
`persistent_resource` |
Required. The PersistentResource to create. |
`persistent_resource_id` |
`str`
Required. The ID to use for the PersistentResource, which become the final component of the PersistentResource's resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreatePersistentResourceRequest

```
CreatePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.CreatePersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleDriveSource.ResourceId.ResourceType -->

# Class ResourceType (1.135.0)

`ResourceType(value)`


The type of the Google Drive resource.

## Enums |
|
|---|---|
Name |
Description |
`RESOURCE_TYPE_UNSPECIFIED` |
Unspecified resource type. |
`RESOURCE_TYPE_FILE` |
File resource type. |
`RESOURCE_TYPE_FOLDER` |
Folder resource type. |

## Methods

### ResourceType

`ResourceType(value)`


The type of the Google Drive resource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.ViewRestApi -->

# Class ViewRestApi (1.135.0)

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

## Attributes |
|
|---|---|
Name |
Description |
`documentations` |
`MutableSequence[`
Required. |
`title` |
`str`
Required. The title of the view rest API. |

## Methods

### ViewRestApi

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schema.PropertiesEntry -->

# Class PropertiesEntry (1.135.0)

`PropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### PropertiesEntry

`PropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.VertexRagSource -->

# Class VertexRagSource (1.135.0)

`VertexRagSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Vertex Rag source for features that need to be synced to Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
Required. The BigQuery view/table URI that will be materialized on each manual sync trigger. The table/view is expected to have the following columns and types at least: - `corpus_id` (STRING, NULLABLE/REQUIRED)
- `file_id` (STRING, NULLABLE/REQUIRED)
- `chunk_id` (STRING, NULLABLE/REQUIRED)
- `chunk_data_type` (STRING, NULLABLE/REQUIRED)
- `chunk_data` (STRING, NULLABLE/REQUIRED)
- `embeddings` (FLOAT, REPEATED)
- `file_original_uri` (STRING, NULLABLE/REQUIRED)
|
`rag_corpus_id` |
`int`
Optional. The RAG corpus id corresponding to this FeatureView. |

## Methods

### VertexRagSource

`VertexRagSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Vertex Rag source for features that need to be synced to Online Store.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictRequestResponseLoggingConfig -->

# Class PredictRequestResponseLoggingConfig (1.135.0)

```
PredictRequestResponseLoggingConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for logging request-response to a BigQuery table.

## Attributes |
|
|---|---|
Name |
Description |
`enabled` |
`bool`
If logging is enabled or not. |
`sampling_rate` |
`float`
Percentage of requests to be logged, expressed as a fraction in range(0,1]. |
`bigquery_destination` |
BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_` where will
be made BigQuery-dataset-name compatible (e.g. most special
characters will become underscores). If no table name is
given, a new table will be created with name
`request_response_logging`
|

## Methods

### PredictRequestResponseLoggingConfig

```
PredictRequestResponseLoggingConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for logging request-response to a BigQuery table.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadataOverride.InputsEntry -->

# Class InputsEntry (1.135.0)

`InputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### InputsEntry

`InputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitoringJobRequest -->

# Class CreateModelMonitoringJobRequest (1.135.0)

```
CreateModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.CreateModelMonitoringJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelMonitoringJob. Format: `projects/{project}/locations/{location}/modelMoniitors/{model_monitor}`
|
`model_monitoring_job` |
Required. The ModelMonitoringJob to create |
`model_monitoring_job_id` |
`str`
Optional. The ID to use for the Model Monitoring Job, which will become the final component of the model monitoring job resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreateModelMonitoringJobRequest

```
CreateModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.CreateModelMonitoringJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsRequest -->

# Class SearchModelMonitoringStatsRequest (1.135.0)

```
SearchModelMonitoringStatsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.SearchModelMonitoringStats.

## Attributes |
|
|---|---|
Name |
Description |
`model_monitor` |
`str`
Required. ModelMonitor resource name. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}`
|
`stats_filter` |
Filter for search different stats. |
`time_interval` |
`google.type.interval_pb2.Interval`
The time interval for which results should be returned. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
A page token received from a previous ModelMonitoringService.SearchModelMonitoringStats call. |

## Methods

### SearchModelMonitoringStatsRequest

```
SearchModelMonitoringStatsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.SearchModelMonitoringStats.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AnnotationSpec -->

# Class AnnotationSpec (1.135.0)

`AnnotationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Identifies a concept with which DataItems may be annotated with.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the AnnotationSpec. |
`display_name` |
`str`
Required. The user-defined name of the AnnotationSpec. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this AnnotationSpec was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when AnnotationSpec was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |

## Methods

### AnnotationSpec

`AnnotationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Identifies a concept with which DataItems may be annotated with.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob.LabelsEntry -->

# Class LabelsEntry (1.135.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.OpenSourceCategory -->

# Class OpenSourceCategory (1.135.0)

`OpenSourceCategory(value)`


An enum representing the open source category of a PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`OPEN_SOURCE_CATEGORY_UNSPECIFIED` |
The open source category is unspecified, which should not be used. |
`PROPRIETARY` |
Used to indicate the PublisherModel is not open sourced. |
`GOOGLE_OWNED_OSS_WITH_GOOGLE_CHECKPOINT` |
Used to indicate the PublisherModel is a Google-owned open source model w/ Google checkpoint. |
`THIRD_PARTY_OWNED_OSS_WITH_GOOGLE_CHECKPOINT` |
Used to indicate the PublisherModel is a 3p-owned open source model w/ Google checkpoint. |
`GOOGLE_OWNED_OSS` |
Used to indicate the PublisherModel is a Google-owned pure open source model. |
`THIRD_PARTY_OWNED_OSS` |
Used to indicate the PublisherModel is a 3p-owned pure open source model. |

## Methods

### OpenSourceCategory

`OpenSourceCategory(value)`


An enum representing the open source category of a PublisherModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyResult -->

# Class SafetyResult (1.135.0)

`SafetyResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Safety score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for safety score. |
`confidence` |
`float`
Output only. Confidence for safety score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SafetyResult

`SafetyResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFilterSplit -->

# Class ExportFilterSplit (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResourceRuntime.AccessUrisEntry -->

# Class AccessUrisEntry (1.135.0)

`AccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### AccessUrisEntry

`AccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RayLogsSpec -->

# Class RayLogsSpec (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeResponse -->

# Class StartNotebookRuntimeResponse (1.135.0)

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

## Methods

### StartNotebookRuntimeResponse

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitor -->

# Class FeatureMonitor (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsRequest -->

# Class UpsertDatapointsRequest (1.135.0)

`UpsertDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpsertDatapoints

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`str`
Required. The name of the Index resource to be updated. Format: `projects/{project}/locations/{location}/indexes/{index}`
|
`datapoints` |
`MutableSequence[`
A list of datapoints to be created/updated. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Update mask is used to specify the fields to be overwritten in the datapoints by the update. The fields specified in the update_mask are relative to each IndexDatapoint inside datapoints, not the full request. Updatable fields: - Use `all_restricts` to update both restricts and
numeric_restricts.
|

## Methods

### UpsertDatapointsRequest

`UpsertDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpsertDatapoints

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint.CrowdingTag -->

# Class CrowdingTag (1.135.0)

`CrowdingTag(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute.

## Attribute |
|
|---|---|
Name |
Description |
`crowding_attribute` |
`str`
The attribute value used for crowding. The maximum number of neighbors to return per crowding attribute value (per_crowding_attribute_num_neighbors) is configured per-query. This field is ignored if per_crowding_attribute_num_neighbors is larger than the total number of neighbors to return for a given query. |

## Methods

### CrowdingTag

`CrowdingTag(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsRequest -->

# Class QueryDeployedModelsRequest (1.135.0)

`QueryDeployedModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for QueryDeployedModels method.

## Attributes |
|
|---|---|
Name |
Description |
`deployment_resource_pool` |
`str`
Required. The name of the target DeploymentResourcePool to query. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|
`page_size` |
`int`
The maximum number of DeployedModels to return. The service may return fewer than this value. |
`page_token` |
`str`
A page token, received from a previous `QueryDeployedModels` call. Provide this to retrieve the
subsequent page.
When paginating, all other parameters provided to
`QueryDeployedModels` must match the call that provided
the page token.
|

## Methods

### QueryDeployedModelsRequest

`QueryDeployedModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for QueryDeployedModels method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SharePointSources -->

# Class SharePointSources (1.135.0)

`SharePointSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The SharePointSources to pass to ImportRagFiles.

## Attribute |
|
|---|---|
Name |
Description |
`share_point_sources` |
`MutableSequence[`
The SharePoint sources. |

## Classes

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### SharePointSources

`SharePointSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The SharePointSources to pass to ImportRagFiles.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingMetadata -->

# Class GroundingMetadata (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types -->

# Package instance_v1.types (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Feature.MonitoringStatsAnomaly -->

# Class MonitoringStatsAnomaly (1.135.0)

`MonitoringStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of historical SnapshotAnalysis or ImportFeaturesAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending.

## Attributes |
|
|---|---|
Name |
Description |
`objective` |
Output only. The objective for each stats. |
`feature_stats_anomaly` |
Output only. The stats and anomalies generated at specific timestamp. |

## Classes

### Objective

`Objective(value)`


If the objective in the request is both Import Feature Analysis and Snapshot Analysis, this objective could be one of them. Otherwise, this objective should be the same as the objective in the request.

## Methods

### MonitoringStatsAnomaly

`MonitoringStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of historical SnapshotAnalysis or ImportFeaturesAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VertexRagSource -->

# Class VertexRagSource (1.135.0)

`VertexRagSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Vertex Rag source for features that need to be synced to Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
Required. The BigQuery view/table URI that will be materialized on each manual sync trigger. The table/view is expected to have the following columns and types at least: - `corpus_id` (STRING, NULLABLE/REQUIRED)
- `file_id` (STRING, NULLABLE/REQUIRED)
- `chunk_id` (STRING, NULLABLE/REQUIRED)
- `chunk_data_type` (STRING, NULLABLE/REQUIRED)
- `chunk_data` (STRING, NULLABLE/REQUIRED)
- `embeddings` (FLOAT, REPEATED)
- `file_original_uri` (STRING, NULLABLE/REQUIRED)
|
`rag_corpus_id` |
`int`
Optional. The RAG corpus id corresponding to this FeatureView. |

## Methods

### VertexRagSource

`VertexRagSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Vertex Rag source for features that need to be synced to Online Store.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKeyMatchMetricValue -->

# Class ToolParameterKeyMatchMetricValue (1.135.0)

```
ToolParameterKeyMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool parameter key match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolParameterKeyMatchMetricValue

```
ToolParameterKeyMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CsvDestination -->

# Class CsvDestination (1.135.0)

`CsvDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV output content.

## Attribute |
|
|---|---|
Name |
Description |
`gcs_destination` |
Required. Google Cloud Storage location. |

## Methods

### CsvDestination

`CsvDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV output content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RougeInput -->

# Class RougeInput (1.135.0)

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for rouge score metric. |
`instances` |
`MutableSequence[`
Required. Repeated rouge instances. |

## Methods

### RougeInput

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient -->

# Class GenAiCacheServiceAsyncClient (1.135.0)

```
GenAiCacheServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for managing Vertex AI's CachedContent resource.

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
`GenAiCacheServiceTransport` |
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

### GenAiCacheServiceAsyncClient

```
GenAiCacheServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai cache service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,GenAiCacheServiceTransport,Callable[..., GenAiCacheServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiCacheServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_cached_content

```
create_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.CreateCachedContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
cached_content: typing.Optional[
google.cloud.aiplatform_v1.types.cached_content.CachedContent
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.cached_content.CachedContent
```


Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_cached_content():
# Create a client
client = aiplatform_v1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateCachedContentRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_create_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.CreateCachedContent. |
`parent` |
Required. The parent resource where the cached content will be created This corresponds to the |
`cached_content` |
Required. The cached content to create This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

### delete_cached_content

```
delete_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.DeleteCachedContentRequest,
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
) -> None
```


Deletes cached content

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_cached_content():
# Create a client
client = aiplatform_v1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteCachedContentRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_delete_cached_content)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.DeleteCachedContent. |
`name` |
Required. The resource name referring to the cached content This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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
`GenAiCacheServiceAsyncClient` |
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
`GenAiCacheServiceAsyncClient` |
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
`GenAiCacheServiceAsyncClient` |
The constructed client. |

### get_cached_content

```
get_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.GetCachedContentRequest,
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
) -> google.cloud.aiplatform_v1.types.cached_content.CachedContent
```


Gets cached content configurations

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_cached_content():
# Create a client
client = aiplatform_v1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetCachedContentRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_get_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.GetCachedContent. |
`name` |
Required. The resource name referring to the cached content This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

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
google.cloud.aiplatform_v1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport
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

### list_cached_contents

```
list_cached_contents(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsRequest,
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
google.cloud.aiplatform_v1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager
)
```


Lists cached contents in a project

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_cached_contents():
# Create a client
client = aiplatform_v1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListCachedContentsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_cached_contents](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_list_cached_contents)(request=request)
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
The request object. Request to list CachedContents. |
`parent` |
Required. The parent, which owns this collection of cached contents. This corresponds to the |
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
Response with a list of CachedContents. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_cached_content

```
update_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.UpdateCachedContentRequest,
dict,
]
] = None,
*,
cached_content: typing.Optional[
google.cloud.aiplatform_v1.types.cached_content.CachedContent
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
) -> google.cloud.aiplatform_v1.types.cached_content.CachedContent
```


Updates cached content configurations

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_cached_content():
# Create a client
client = aiplatform_v1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateCachedContentRequest.html)(
)
# Make the request
response = await client.[update_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_update_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated. |
`cached_content` |
Required. The cached content to update This corresponds to the |
`update_mask` |
Required. The list of fields to update. This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient -->

# Class NotebookServiceClient (1.135.0)

```
NotebookServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### NotebookServiceClient

```
NotebookServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the notebook service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the NotebookServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_assign_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
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
operation = client.[assign_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_assign_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.AssignNotebookRuntime. |
`parent` |
`str`
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: |
`notebook_runtime_template` |
`str`
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). This corresponds to the |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. This corresponds to the |
`notebook_runtime_id` |
`str`
Optional. User specified ID for the notebook runtime. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
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
operation = client.[create_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_create_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.CreateNotebookExecutionJob] |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookExecutionJob. Format: |
`notebook_execution_job` |
Required. The NotebookExecutionJob to create. This corresponds to the |
`notebook_execution_job_id` |
`str`
Optional. User specified ID for the NotebookExecutionJob. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateRequest.html)(
parent="parent_value",
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
operation = client.[create_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_create_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.CreateNotebookRuntimeTemplate. |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. This corresponds to the |
`notebook_runtime_template_id` |
`str`
Optional. User specified ID for the notebook runtime template. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_delete_notebook_execution_job)(request=request)
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
The request object. Request message for [NotebookService.DeleteNotebookExecutionJob] |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource to be deleted. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_delete_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_delete_notebook_runtime_template)(request=request)
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
The request object. Request message for NotebookService.DeleteNotebookRuntimeTemplate. |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: |
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
`NotebookServiceClient` |
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
`NotebookServiceClient` |
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
`NotebookServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_notebook_execution_job():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookExecutionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookExecutionJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_notebook_execution_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_get_notebook_execution_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [NotebookService.GetNotebookExecutionJob] |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_get_notebook_runtime)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for NotebookService.GetNotebookRuntime |
`name` |
`str`
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_get_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for NotebookService.GetNotebookRuntimeTemplate |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsPager
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
def sample_list_notebook_execution_jobs():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookExecutionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_execution_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_list_notebook_execution_jobs)(request=request)
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
The request object. Request message for [NotebookService.ListNotebookExecutionJobs] |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager
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
def sample_list_notebook_runtime_templates():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimeTemplatesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtime_templates](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_list_notebook_runtime_templates)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimeTemplates. |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesPager
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
def sample_list_notebook_runtimes():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNotebookRuntimesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_notebook_runtimes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_list_notebook_runtimes)(request=request)
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
The request object. Request message for NotebookService.ListNotebookRuntimes. |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_start_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StartNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[start_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_start_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StartNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_stop_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StopNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[stop_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_stop_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.StopNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_update_notebook_runtime_template():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
notebook_runtime_template = aiplatform_v1beta1.[NotebookRuntimeTemplate](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.html)()
notebook_runtime_template.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateNotebookRuntimeTemplateRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateNotebookRuntimeTemplateRequest.html)(
notebook_runtime_template=notebook_runtime_template,
)
# Make the request
response = client.[update_notebook_runtime_template](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_update_notebook_runtime_template)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for NotebookService.UpdateNotebookRuntimeTemplate. |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_upgrade_notebook_runtime():
# Create a client
client = aiplatform_v1beta1.
```[NotebookServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpgradeNotebookRuntimeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[upgrade_notebook_runtime](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient.html#google_cloud_aiplatform_v1beta1_services_notebook_service_NotebookServiceClient_upgrade_notebook_runtime)(request=request)
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
The request object. Request message for NotebookService.UpgradeNotebookRuntime. |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. This corresponds to the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.135.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FluencyResult -->

# Class FluencyResult (1.135.0)

`FluencyResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Fluency score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for fluency score. |
`confidence` |
`float`
Output only. Confidence for fluency score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### FluencyResult

`FluencyResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJob -->

# Class ModelMonitoringJob (1.135.0)

`ModelMonitoringJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a model monitoring job that analyze dataset using different monitoring algorithm.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a ModelMonitoringJob. Format: `projects/{project_id}/locations/{location_id}/modelMonitors/{model_monitor_id}/modelMonitoringJobs/{model_monitoring_job_id}`
|
`display_name` |
`str`
The display name of the ModelMonitoringJob. The name can be up to 128 characters long and can consist of any UTF-8. |
`model_monitoring_spec` |
Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports. If left blank, the default monitoring specifications from the top-level resource 'ModelMonitor' will be applied. If provided, we will use the specification defined here rather than the default one. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelMonitoringJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelMonitoringJob was updated most recently. |
`state` |
Output only. The state of the monitoring job. - When the job is still creating, the state will be 'JOB_STATE_PENDING'. - Once the job is successfully created, the state will be 'JOB_STATE_RUNNING'. - Once the job is finished, the state will be one of 'JOB_STATE_FAILED', 'JOB_STATE_SUCCEEDED', 'JOB_STATE_PARTIALLY_SUCCEEDED'. |
`schedule` |
`str`
Output only. Schedule resource name. It will only appear when this job is triggered by a schedule. |
`job_execution_detail` |
Output only. Execution results for all the monitoring objectives. |
`schedule_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelMonitoringJob was scheduled. It will only appear when this job is triggered by a schedule. |

## Methods

### ModelMonitoringJob

`ModelMonitoringJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a model monitoring job that analyze dataset using different monitoring algorithm.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact.PropertiesEntry -->

# Class PropertiesEntry (1.135.0)

`PropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### PropertiesEntry

`PropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourceRuntime.AccessUrisEntry -->

# Class AccessUrisEntry (1.135.0)

`AccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### AccessUrisEntry

`AccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamQueryReasoningEngineRequest -->

# Class StreamQueryReasoningEngineRequest (1.135.0)

```
StreamQueryReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [ReasoningEngineExecutionService.StreamQuery][].

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`input` |
`google.protobuf.struct_pb2.Struct`
Optional. Input content provided by users in JSON object format. Examples include text query, function calling parameters, media bytes, etc. |
`class_method` |
`str`
Optional. Class method to be used for the stream query. It is optional and defaults to "stream_query" if unspecified. |

## Methods

### StreamQueryReasoningEngineRequest

```
StreamQueryReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [ReasoningEngineExecutionService.StreamQuery][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial.WebAccessUrisEntry -->

# Class WebAccessUrisEntry (1.135.0)

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SharePointSources -->

# Class SharePointSources (1.135.0)

`SharePointSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The SharePointSources to pass to ImportRagFiles.

## Attribute |
|
|---|---|
Name |
Description |
`share_point_sources` |
`MutableSequence[`
The SharePoint sources. |

## Classes

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### SharePointSources

`SharePointSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The SharePointSources to pass to ImportRagFiles.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.ConfigsEntry -->

# Class ConfigsEntry (1.135.0)

`ConfigsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ConfigsEntry

`ConfigsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Feature.MonitoringStatsAnomaly -->

# Class MonitoringStatsAnomaly (1.135.0)

`MonitoringStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of historical SnapshotAnalysis or ImportFeaturesAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending.

## Attributes |
|
|---|---|
Name |
Description |
`objective` |
Output only. The objective for each stats. |
`feature_stats_anomaly` |
Output only. The stats and anomalies generated at specific timestamp. |

## Classes

### Objective

`Objective(value)`


If the objective in the request is both Import Feature Analysis and Snapshot Analysis, this objective could be one of them. Otherwise, this objective should be the same as the objective in the request.

## Methods

### MonitoringStatsAnomaly

`MonitoringStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of historical SnapshotAnalysis or ImportFeaturesAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Presets.Query -->

# Class Query (1.135.0)

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Enums |
|
|---|---|
Name |
Description |
`PRECISE` |
More precise neighbors as a trade-off against slower response. |
`FAST` |
Faster response as a trade-off against less precise neighbors. |

## Methods

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesResponse -->

# Class WriteFeatureValuesResponse (1.135.0)

`WriteFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

## Methods

### WriteFeatureValuesResponse

`WriteFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.ViewRestApi -->

# Class ViewRestApi (1.135.0)

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

## Attributes |
|
|---|---|
Name |
Description |
`documentations` |
`MutableSequence[`
Required. |
`title` |
`str`
Required. The title of the view rest API. |

## Methods

### ViewRestApi

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Event.Type -->

# Class Type (1.135.0)

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Unspecified whether input or output of the Execution. |
`INPUT` |
An input of the Execution. |
`OUTPUT` |
An output of the Execution. |

## Methods

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.135.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchMetricValue -->

# Class TrajectoryInOrderMatchMetricValue (1.135.0)

```
TrajectoryInOrderMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryInOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectoryInOrderMatch score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectoryInOrderMatchMetricValue

```
TrajectoryInOrderMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryInOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.135.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Examples -->

# Class Examples (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsRequest -->

# Class ListFeatureViewsRequest (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchMetricValue -->

# Class ToolParameterKeyMatchMetricValue (1.135.0)

```
ToolParameterKeyMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool parameter key match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolParameterKeyMatchMetricValue

```
ToolParameterKeyMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJob.WebAccessUrisEntry -->

# Class WebAccessUrisEntry (1.135.0)

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SupervisedTuningSpec -->

# Class SupervisedTuningSpec (1.135.0)

`SupervisedTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Supervised Tuning for first party models.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset_uri` |
`str`
Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file. |
`validation_dataset_uri` |
`str`
Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file. |
`hyper_parameters` |
Optional. Hyperparameters for SFT. |
`export_last_checkpoint_only` |
`bool`
Optional. If set to true, disable intermediate checkpoints for SFT and only the last checkpoint will be exported. Otherwise, enable intermediate checkpoints for SFT. Default is false. |

## Methods

### SupervisedTuningSpec

`SupervisedTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Supervised Tuning for first party models.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FullFineTunedResources -->

# Class FullFineTunedResources (1.135.0)

`FullFineTunedResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Resources for an fft model.

## Attributes |
|
|---|---|
Name |
Description |
`deployment_type` |
Required. The kind of deployment. |
`model_inference_unit_count` |
`int`
Optional. The number of model inference units to use for this deployment. This can only be specified for DEPLOYMENT_TYPE_PROD. The following table lists the number of model inference units for different model types: - Gemini 2.5 Flash - Foundation FMIU: 25 - Expansion FMIU: 4 - Gemini 2.5 Pro - Foundation FMIU: 32 - Expansion FMIU: 16 - Veo 3.0 (undistilled) - Foundation FMIU: 63 - Expansion FMIU: 7 - Veo 3.0 (distilled) - Foundation FMIU: 30 - Expansion FMIU: 10 |

## Classes

### DeploymentType

`DeploymentType(value)`


The type of deployment.

## Methods

### FullFineTunedResources

`FullFineTunedResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Resources for an fft model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometResult -->

# Class CometResult (1.135.0)

`CometResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Comet score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### CometResult

`CometResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencyResult -->

# Class FluencyResult (1.135.0)

`FluencyResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Fluency score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for fluency score. |
`confidence` |
`float`
Output only. Confidence for fluency score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### FluencyResult

`FluencyResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsRequest -->

# Class ListFeatureViewsRequest (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchInstance -->

# Class ExactMatchInstance (1.135.0)

`ExactMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ExactMatchInstance

`ExactMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.ParametersEntry -->

# Class ParametersEntry (1.135.0)

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ParametersEntry

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial.WebAccessUrisEntry -->

# Class WebAccessUrisEntry (1.135.0)

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamQueryReasoningEngineRequest -->

# Class StreamQueryReasoningEngineRequest (1.135.0)

```
StreamQueryReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [ReasoningEngineExecutionService.StreamQuery][].

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`input` |
`google.protobuf.struct_pb2.Struct`
Optional. Input content provided by users in JSON object format. Examples include text query, function calling parameters, media bytes, etc. |
`class_method` |
`str`
Optional. Class method to be used for the stream query. It is optional and defaults to "stream_query" if unspecified. |

## Methods

### StreamQueryReasoningEngineRequest

```
StreamQueryReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [ReasoningEngineExecutionService.StreamQuery][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient -->

# Class GenAiCacheServiceAsyncClient (1.135.0)

```
GenAiCacheServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for managing Vertex AI's CachedContent resource.

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
`GenAiCacheServiceTransport` |
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

### GenAiCacheServiceAsyncClient

```
GenAiCacheServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai cache service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,GenAiCacheServiceTransport,Callable[..., GenAiCacheServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiCacheServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_cached_content

```
create_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.CreateCachedContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
cached_content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
```


Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCachedContentRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_create_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.CreateCachedContent. |
`parent` |
Required. The parent resource where the cached content will be created This corresponds to the |
`cached_content` |
Required. The cached content to create This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

### delete_cached_content

```
delete_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.DeleteCachedContentRequest,
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
) -> None
```


Deletes cached content

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCachedContentRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_delete_cached_content)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.DeleteCachedContent. |
`name` |
Required. The resource name referring to the cached content This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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
`GenAiCacheServiceAsyncClient` |
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
`GenAiCacheServiceAsyncClient` |
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
`GenAiCacheServiceAsyncClient` |
The constructed client. |

### get_cached_content

```
get_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.GetCachedContentRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
```


Gets cached content configurations

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCachedContentRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_get_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.GetCachedContent. |
`name` |
Required. The resource name referring to the cached content This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

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
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport
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

### list_cached_contents

```
list_cached_contents(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
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
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager
)
```


Lists cached contents in a project

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_cached_contents():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListCachedContentsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_cached_contents](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_list_cached_contents)(request=request)
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
The request object. Request to list CachedContents. |
`parent` |
Required. The parent, which owns this collection of cached contents. This corresponds to the |
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
Response with a list of CachedContents. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_cached_content

```
update_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.UpdateCachedContentRequest,
dict,
]
] = None,
*,
cached_content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
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
) -> google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
```


Updates cached content configurations

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateCachedContentRequest.html)(
)
# Make the request
response = await client.[update_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_update_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated. |
`cached_content` |
Required. The cached content to update This corresponds to the |
`update_mask` |
Required. The list of fields to update. This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient -->

# Class GenAiCacheServiceAsyncClient (1.134.0)

```
GenAiCacheServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for managing Vertex AI's CachedContent resource.

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
`GenAiCacheServiceTransport` |
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

### GenAiCacheServiceAsyncClient

```
GenAiCacheServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai cache service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,GenAiCacheServiceTransport,Callable[..., GenAiCacheServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiCacheServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_cached_content

```
create_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.CreateCachedContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
cached_content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
```


Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCachedContentRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_create_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.CreateCachedContent. |
`parent` |
Required. The parent resource where the cached content will be created This corresponds to the |
`cached_content` |
Required. The cached content to create This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

### delete_cached_content

```
delete_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.DeleteCachedContentRequest,
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
) -> None
```


Deletes cached content

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCachedContentRequest.html)(
name="name_value",
)
# Make the request
await client.[delete_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_delete_cached_content)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.DeleteCachedContent. |
`name` |
Required. The resource name referring to the cached content This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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
`GenAiCacheServiceAsyncClient` |
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
`GenAiCacheServiceAsyncClient` |
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
`GenAiCacheServiceAsyncClient` |
The constructed client. |

### get_cached_content

```
get_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.GetCachedContentRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
```


Gets cached content configurations

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCachedContentRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_get_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.GetCachedContent. |
`name` |
Required. The resource name referring to the cached content This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

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
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.transports.base.GenAiCacheServiceTransport
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

### list_cached_contents

```
list_cached_contents(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
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
google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager
)
```


Lists cached contents in a project

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_cached_contents():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListCachedContentsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_cached_contents](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_list_cached_contents)(request=request)
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
The request object. Request to list CachedContents. |
`parent` |
Required. The parent, which owns this collection of cached contents. This corresponds to the |
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
Response with a list of CachedContents. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_cached_content

```
update_cached_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.UpdateCachedContentRequest,
dict,
]
] = None,
*,
cached_content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
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
) -> google.cloud.aiplatform_v1beta1.types.cached_content.CachedContent
```


Updates cached content configurations

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_cached_content():
# Create a client
client = aiplatform_v1beta1.
```[GenAiCacheServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateCachedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateCachedContentRequest.html)(
)
# Make the request
response = await client.[update_cached_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_cache_service_GenAiCacheServiceAsyncClient_update_cached_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated. |
`cached_content` |
Required. The cached content to update This corresponds to the |
`update_mask` |
Required. The list of fields to update. This corresponds to the |
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
A resource used in LLM queries for users to explicitly specify what to cache and how to cache. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.TimestampTransformation -->

# Class TimestampTransformation (1.134.0)

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


## Attribute |
|
|---|---|
Name |
Description |
`time_format` |
`str`
The format in which that time field is expressed. The time_format must either be one of: - `unix-seconds`
- `unix-milliseconds`
- `unix-microseconds`
- `unix-nanoseconds`
(for respectively number of seconds, milliseconds,
microseconds and nanoseconds since start of the Unix epoch);
or be written in `strftime` syntax.
If time_format is not set, then the default format is RFC
3339 `date-time` format, where `time-offset` = `"Z"`
(e.g. 1985-04-12T23:20:50.52Z)
|

## Methods

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.ConfigsEntry -->

# Class ConfigsEntry (1.134.0)

`ConfigsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ConfigsEntry

`ConfigsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeResponse -->

# Class StartNotebookRuntimeResponse (1.134.0)

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

## Methods

### StartNotebookRuntimeResponse

```
StartNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.ModelMonitoringDataset.ModelMonitoringGcsSource.DataFormat -->

# Class DataFormat (1.134.0)

`DataFormat(value)`


Supported data format.

## Enums |
|
|---|---|
Name |
Description |
`DATA_FORMAT_UNSPECIFIED` |
Data format unspecified, used when this field is unset. |
`CSV` |
CSV files. |
`TF_RECORD` |
TfRecord files |
`JSONL` |
JsonL files. |

## Methods

### DataFormat

`DataFormat(value)`


Supported data format.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextSentimentPredictionResult -->

# Class TextSentimentPredictionResult (1.134.0)

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

## Attribute |
|
|---|---|
Name |
Description |
`sentiment` |
`int`
The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive). |

## Methods

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsRequest -->

# Class ListCachedContentsRequest (1.134.0)

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent, which owns this collection of cached contents. |
`page_size` |
`int`
Optional. The maximum number of cached contents to return. The service may return fewer than this value. If unspecified, some default (under maximum) number of items will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000. |
`page_token` |
`str`
Optional. A page token, received from a previous `ListCachedContents` call. Provide this to retrieve the
subsequent page.
When paginating, all other parameters provided to
`ListCachedContents` must match the call that provided the
page token.
|

## Methods

### ListCachedContentsRequest

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore -->

# Class ExampleStore (1.134.0)

`ExampleStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an executable service to manage and retrieve examples.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the ExampleStore. This is a unique identifier. Format: projects/{project}/locations/{location}/exampleStores/{example_store} |
`display_name` |
`str`
Required. Display name of the ExampleStore. |
`description` |
`str`
Optional. Description of the ExampleStore. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ExampleStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ExampleStore was most recently updated. |
`example_store_config` |
Required. Example Store config. |

## Methods

### ExampleStore

`ExampleStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an executable service to manage and retrieve examples.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest.SnapshotExport -->

# Class SnapshotExport (1.134.0)

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

## Attributes |
|
|---|---|
Name |
Description |
`snapshot_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Exports Feature values as of this timestamp. If not set, retrieve values as of now. Timestamp, if present, must not have higher than millisecond precision. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Methods

### SnapshotExport

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult -->

# Class VideoObjectTrackingPredictionResult (1.134.0)

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |
`frames` |
`MutableSequence[`
All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object. |

## Classes

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

## Methods

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec.EmailConfig -->

# Class EmailConfig (1.134.0)

`EmailConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alerts.

## Attribute |
|
|---|---|
Name |
Description |
`user_emails` |
`MutableSequence[str]`
The email addresses to send the alerts. |

## Methods

### EmailConfig

`EmailConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alerts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample.SearchKeyGenerationMethod.LastEntry -->

# Class LastEntry (1.134.0)

`LastEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for using only the last entry of the conversation history as the search key.

## Methods

### LastEntry

`LastEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for using only the last entry of the conversation history as the search key.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest -->

# Class CompleteTrialRequest (1.134.0)

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|
`final_measurement` |
Optional. If provided, it will be used as the completed Trial's final_measurement; Otherwise, the service will auto-select a previously reported measurement as the final-measurement |
`trial_infeasible` |
`bool`
Optional. True if the Trial cannot be run with the given Parameter, and final_measurement will be ignored. |
`infeasible_reason` |
`str`
Optional. A human readable reason why the trial was infeasible. This should only be provided if `trial_infeasible` is true.
|

## Methods

### CompleteTrialRequest

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.134.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service -->

# Package vizier_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.vizier_service`

package.

## Classes

[VizierServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceAsyncClient)

Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

[VizierServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.VizierServiceClient)

Vertex AI Vizier API.

Vertex AI Vizier is a service to solve blackbox optimization problems, such as tuning machine learning hyperparameters and searching over deep learning architectures.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers)

API documentation for `aiplatform_v1beta1.services.vizier_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service -->

# Package model_monitoring_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.model_monitoring_service`

package.

## Classes

[ModelMonitoringServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceAsyncClient)

A service for creating and managing Vertex AI Model moitoring. This
includes `ModelMonitor`

resources, `ModelMonitoringJob`

resources.

[ModelMonitoringServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient)

A service for creating and managing Vertex AI Model moitoring. This
includes `ModelMonitor`

resources, `ModelMonitoringJob`

resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers)

API documentation for `aiplatform_v1beta1.services.model_monitoring_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RolloutOptions -->

# Class RolloutOptions (1.134.0)

`RolloutOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for rolling deployments.

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
`max_unavailable_replicas` |
`int`
Absolute count of replicas allowed to be unavailable. This field is a member of `oneof` _ `max_unavailable` .
|
`max_unavailable_percentage` |
`int`
Percentage of replicas allowed to be unavailable. For autoscaling deployments, this refers to the target replica count. This field is a member of `oneof` _ `max_unavailable` .
|
`max_surge_replicas` |
`int`
Absolute count of allowed additional replicas. This field is a member of `oneof` _ `max_surge` .
|
`max_surge_percentage` |
`int`
Percentage of allowed additional replicas. For autoscaling deployments, this refers to the target replica count. This field is a member of `oneof` _ `max_surge` .
|
`previous_deployed_model` |
`str`
ID of the DeployedModel that this deployment should replace. |
`revision_number` |
`int`
Output only. Read-only. Revision number determines the relative priority of DeployedModels in the same rollout. The DeployedModel with the largest revision number specifies the intended state of the deployment. |

## Methods

### RolloutOptions

`RolloutOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for rolling deployments.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeInput -->

# Class RougeInput (1.134.0)

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for rouge score metric. |
`instances` |
`MutableSequence[`
Required. Repeated rouge instances. |

## Methods

### RougeInput

`RougeInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for rouge metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveContextChildrenResponse -->

# Class RemoveContextChildrenResponse (1.134.0)

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

## Methods

### RemoveContextChildrenResponse

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob.WebAccessUrisEntry -->

# Class WebAccessUrisEntry (1.134.0)

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometResult -->

# Class CometResult (1.134.0)

`CometResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Comet score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### CometResult

`CometResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.Deploy.DeployMetadata.LabelsEntry -->

# Class LabelsEntry (1.134.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs.ArtifactsEntry -->

# Class ArtifactsEntry (1.134.0)

`ArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ArtifactsEntry

`ArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchMetricValue -->

# Class TrajectoryAnyOrderMatchMetricValue (1.134.0)

```
TrajectoryAnyOrderMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryAnyOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectoryAnyOrderMatch score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectoryAnyOrderMatchMetricValue

```
TrajectoryAnyOrderMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryAnyOrderMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.ParametersEntry -->

# Class ParametersEntry (1.134.0)

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ParametersEntry

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesRequest -->

# Class ListEntityTypesRequest (1.134.0)

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Featurestore to list EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`filter` |
`str`
Lists the EntityTypes that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality as well as key
presence.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` -->
EntityTypes having both (active: yes) and (env: prod)
labels.
- `labels.env: *` --> Any EntityType which has a label
with 'env' as the key.
|
`page_size` |
`int`
The maximum number of EntityTypes to return. The service may return fewer than this value. If unspecified, at most 1000 EntityTypes will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListEntityTypes call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListEntityTypes must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `entity_type_id`
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListEntityTypesRequest

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchInstance -->

# Class ExactMatchInstance (1.134.0)

`ExactMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match instance.

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
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ExactMatchInstance

`ExactMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for exact match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseMetricValue -->

# Class TrajectorySingleToolUseMetricValue (1.134.0)

```
TrajectorySingleToolUseMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectorySingleToolUse metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectorySingleToolUse score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectorySingleToolUseMetricValue

```
TrajectorySingleToolUseMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectorySingleToolUse metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsRequest -->

# Class ListCachedContentsRequest (1.134.0)

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent, which owns this collection of cached contents. |
`page_size` |
`int`
Optional. The maximum number of cached contents to return. The service may return fewer than this value. If unspecified, some default (under maximum) number of items will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000. |
`page_token` |
`str`
Optional. A page token, received from a previous `ListCachedContents` call. Provide this to retrieve the
subsequent page.
When paginating, all other parameters provided to
`ListCachedContents` must match the call that provided the
page token.
|

## Methods

### ListCachedContentsRequest

`ListCachedContentsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request to list CachedContents.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets.Query -->

# Class Query (1.134.0)

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Enums |
|
|---|---|
Name |
Description |
`PRECISE` |
More precise neighbors as a trade-off against slower response. |
`FAST` |
Faster response as a trade-off against less precise neighbors. |

## Methods

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceInput -->

# Class CoherenceInput (1.134.0)

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for coherence score metric. |
`instance` |
Required. Coherence instance. |

## Methods

### CoherenceInput

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchMetricValue -->

# Class ToolParameterKVMatchMetricValue (1.134.0)

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool parameter key value match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolParameterKVMatchMetricValue

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest.SnapshotExport -->

# Class SnapshotExport (1.134.0)

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

## Attributes |
|
|---|---|
Name |
Description |
`snapshot_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Exports Feature values as of this timestamp. If not set, retrieve values as of now. Timestamp, if present, must not have higher than millisecond precision. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |

## Methods

### SnapshotExport

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult -->

# Class VideoObjectTrackingPredictionResult (1.134.0)

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |
`frames` |
`MutableSequence[`
All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object. |

## Classes

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

## Methods

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

### VideoObjectTrackingPredictionResult

```
VideoObjectTrackingPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime.RuntimeState -->

# Class RuntimeState (1.134.0)

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Enums |
|
|---|---|
Name |
Description |
`RUNTIME_STATE_UNSPECIFIED` |
Unspecified runtime state. |
`RUNNING` |
NotebookRuntime is in running state. |
`BEING_STARTED` |
NotebookRuntime is in starting state. This is when the runtime is being started from a stopped state. |
`BEING_STOPPED` |
NotebookRuntime is in stopping state. |
`STOPPED` |
NotebookRuntime is in stopped state. |
`BEING_UPGRADED` |
NotebookRuntime is in upgrading state. It is in the middle of upgrading process. |
`ERROR` |
NotebookRuntime was unable to start/stop properly. |
`INVALID` |
NotebookRuntime is in invalid state. Cannot be recovered. |

## Methods

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventActions.ArtifactDeltaEntry -->

# Class ArtifactDeltaEntry (1.134.0)

`ArtifactDeltaEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### ArtifactDeltaEntry

`ArtifactDeltaEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest -->

# Class CompleteTrialRequest (1.134.0)

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|
`final_measurement` |
Optional. If provided, it will be used as the completed Trial's final_measurement; Otherwise, the service will auto-select a previously reported measurement as the final-measurement |
`trial_infeasible` |
`bool`
Optional. True if the Trial cannot be run with the given Parameter, and final_measurement will be ignored. |
`infeasible_reason` |
`str`
Optional. A human readable reason why the trial was infeasible. This should only be provided if `trial_infeasible` is true.
|

## Methods

### CompleteTrialRequest

`CompleteTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CompleteTrial.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Event.Type -->

# Class Type (1.134.0)

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Unspecified whether input or output of the Execution. |
`INPUT` |
An input of the Execution. |
`OUTPUT` |
An output of the Execution. |

## Methods

### Type

`Type(value)`


Describes whether an Event's Artifact is the Execution's input or output.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesResponse -->

# Class WriteFeatureValuesResponse (1.134.0)

`WriteFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

## Methods

### WriteFeatureValuesResponse

`WriteFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.WriteFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesRequest -->

# Class ListEntityTypesRequest (1.134.0)

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Featurestore to list EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`filter` |
`str`
Lists the EntityTypes that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality as well as key
presence.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` -->
EntityTypes having both (active: yes) and (env: prod)
labels.
- `labels.env: *` --> Any EntityType which has a label
with 'env' as the key.
|
`page_size` |
`int`
The maximum number of EntityTypes to return. The service may return fewer than this value. If unspecified, at most 1000 EntityTypes will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListEntityTypes call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListEntityTypes must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `entity_type_id`
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListEntityTypesRequest

`ListEntityTypesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolRequest -->

# Class CreateDeploymentResourcePoolRequest (1.134.0)

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent location resource where this DeploymentResourcePool will be created. Format: `projects/{project}/locations/{location}`
|
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. |
`deployment_resource_pool_id` |
`str`
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreateDeploymentResourcePoolRequest

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse -->

# Class QueryDeployedModelsResponse (1.134.0)

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_models` |
`MutableSequence[`
DEPRECATED Use deployed_model_refs instead. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|
`deployed_model_refs` |
`MutableSequence[`
References to the DeployedModels that share the specified deploymentResourcePool. |
`total_deployed_model_count` |
`int`
The total number of DeployedModels on this DeploymentResourcePool. |
`total_endpoint_count` |
`int`
The total number of Endpoints that have DeployedModels on this DeploymentResourcePool. |

## Methods

### QueryDeployedModelsResponse

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy.DeployMetadata.LabelsEntry -->

# Class LabelsEntry (1.134.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig -->

# Class PredictionDriftDetectionConfig (1.134.0)

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

## Attributes |
|
|---|---|
Name |
Description |
`drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws. |
`attribution_score_drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows. |
`default_drift_threshold` |
Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

### AttributionScoreDriftThresholdsEntry

```
AttributionScoreDriftThresholdsEntry(
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

### DriftThresholdsEntry

`DriftThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiTemplateConfig.FieldMappingEntry -->

# Class FieldMappingEntry (1.134.0)

`FieldMappingEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### FieldMappingEntry

`FieldMappingEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest.TrafficSplitEntry -->

# Class TrafficSplitEntry (1.134.0)

`TrafficSplitEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.DataItemLabelsEntry -->

# Class DataItemLabelsEntry (1.134.0)

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### DataItemLabelsEntry

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextSentimentPredictionResult -->

# Class TextSentimentPredictionResult (1.134.0)

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

## Attribute |
|
|---|---|
Name |
Description |
`sentiment` |
`int`
The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive). |

## Methods

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

### TextSentimentPredictionResult

```
TextSentimentPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Sentiment

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchMetricValue -->

# Class ToolParameterKVMatchMetricValue (1.134.0)

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool parameter key value match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolParameterKVMatchMetricValue

```
ToolParameterKVMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Tool parameter key value match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest.DeployConfig.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.134.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardRequest -->

# Class UpdateTensorboardRequest (1.134.0)

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the Tensorboard resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard` |
Required. The Tensorboard's `name` field is used to
identify the Tensorboard to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### UpdateTensorboardRequest

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeRequest -->

# Class AssignNotebookRuntimeRequest (1.134.0)

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: `projects/{project}/locations/{location}`
|
`notebook_runtime_template` |
`str`
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. |
`notebook_runtime_id` |
`str`
Optional. User specified ID for the notebook runtime. |

## Methods

### AssignNotebookRuntimeRequest

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig -->

# Class PredictionDriftDetectionConfig (1.134.0)

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

## Attributes |
|
|---|---|
Name |
Description |
`drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws. |
`attribution_score_drift_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows. |
`default_drift_threshold` |
Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

### AttributionScoreDriftThresholdsEntry

```
AttributionScoreDriftThresholdsEntry(
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

### DriftThresholdsEntry

`DriftThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime.RuntimeState -->

# Class RuntimeState (1.134.0)

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Enums |
|
|---|---|
Name |
Description |
`RUNTIME_STATE_UNSPECIFIED` |
Unspecified runtime state. |
`RUNNING` |
NotebookRuntime is in running state. |
`BEING_STARTED` |
NotebookRuntime is in starting state. This is when the runtime is being started from a stopped state. |
`BEING_STOPPED` |
NotebookRuntime is in stopping state. |
`STOPPED` |
NotebookRuntime is in stopped state. |
`BEING_UPGRADED` |
NotebookRuntime is in upgrading state. It is in the middle of upgrading process. |
`ERROR` |
NotebookRuntime was unable to start/stop properly. |
`INVALID` |
NotebookRuntime is in invalid state. Cannot be recovered. |

## Methods

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardExperimentRequest -->

# Class CreateTensorboardExperimentRequest (1.134.0)

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`tensorboard_experiment` |
The TensorboardExperiment to create. |
`tensorboard_experiment_id` |
`str`
Required. The ID to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreateTensorboardExperimentRequest

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricResult -->

# Class PointwiseMetricResult (1.134.0)

`PointwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Pointwise metric score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for pointwise metric score. |
`custom_output` |
Output only. Spec for custom output. |

## Methods

### PointwiseMetricResult

`PointwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LogprobsResult -->

# Class LogprobsResult (1.134.0)

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

## Attributes |
|
|---|---|
Name |
Description |
`top_candidates` |
`MutableSequence[`
Length = total number of decoding steps. |
`chosen_candidates` |
`MutableSequence[`
Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates. |

## Classes

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TopCandidates

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.

## Methods

### LogprobsResult

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentInstance -->

# Class FulfillmentInstance (1.134.0)

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

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
`instruction` |
`str`
Required. Inference instruction prompt to compare prediction with. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### FulfillmentInstance

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse -->

# Class QueryDeployedModelsResponse (1.134.0)

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

## Attributes |
|
|---|---|
Name |
Description |
`deployed_models` |
`MutableSequence[`
DEPRECATED Use deployed_model_refs instead. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|
`deployed_model_refs` |
`MutableSequence[`
References to the DeployedModels that share the specified deploymentResourcePool. |
`total_deployed_model_count` |
`int`
The total number of DeployedModels on this DeploymentResourcePool. |
`total_endpoint_count` |
`int`
The total number of Endpoints that have DeployedModels on this DeploymentResourcePool. |

## Methods

### QueryDeployedModelsResponse

`QueryDeployedModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for QueryDeployedModels method.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputInfo -->

# Class OutputInfo (1.134.0)

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the info for output of EvaluationService.EvaluateDataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`gcs_output_directory` |
`str`
Output only. The full path of the Cloud Storage directory created, into which the evaluation results and aggregation results are written. This field is a member of `oneof` _ `output_location` .
|

## Methods

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the info for output of EvaluationService.EvaluateDataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchNearestEntitiesRequest -->

# Class SearchNearestEntitiesRequest (1.134.0)

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`query` |
Required. The query. |
`return_full_entity` |
`bool`
Optional. If set to true, the full entities (including all vector values and metadata) of the nearest neighbors are returned; otherwise only entity id of the nearest neighbors will be returned. Note that returning full entities will significantly increase the latency and cost of the query. |

## Methods

### SearchNearestEntitiesRequest

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolRequest -->

# Class CreateDeploymentResourcePoolRequest (1.134.0)

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent location resource where this DeploymentResourcePool will be created. Format: `projects/{project}/locations/{location}`
|
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. |
`deployment_resource_pool_id` |
`str`
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreateDeploymentResourcePoolRequest

```
CreateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for CreateDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresRequest -->

# Class ListMetadataStoresRequest (1.134.0)

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Location whose MetadataStores should be listed. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of Metadata Stores to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListMetadataStores call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |

## Methods

### ListMetadataStoresRequest

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Bigtable -->

# Class Bigtable (1.134.0)

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`auto_scaling` |
Required. Autoscaling config applied to Bigtable Instance. |
`enable_direct_bigtable_access` |
`bool`
If true, enable direct access to the Bigtable instance. |
`bigtable_metadata` |
Metadata of the Bigtable instance. Output only. |
`zone` |
`str`
Optional. The zone where the underlying Bigtable cluster for the primary Bigtable instance will be provisioned. Only the zone must be provided. For example, only "us-central1-a" should be provided. |

## Classes

### AutoScaling

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

## Methods

### Bigtable

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceResult -->

# Class CoherenceResult (1.134.0)

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Coherence score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for coherence score. |
`confidence` |
`float`
Output only. Confidence for coherence score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### CoherenceResult

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseChoice -->

# Class PairwiseChoice (1.134.0)

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

## Enums |
|
|---|---|
Name |
Description |
`PAIRWISE_CHOICE_UNSPECIFIED` |
Unspecified prediction choice. |
`BASELINE` |
Baseline prediction wins |
`CANDIDATE` |
Candidate prediction wins |
`TIE` |
Winner cannot be determined |

## Methods

### PairwiseChoice

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveContextChildrenResponse -->

# Class RemoveContextChildrenResponse (1.134.0)

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

## Methods

### RemoveContextChildrenResponse

```
RemoveContextChildrenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MetadataService.RemoveContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesPayload.FeatureValuesEntry -->

# Class FeatureValuesEntry (1.134.0)

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ActiveLearningConfig -->

# Class ActiveLearningConfig (1.134.0)

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

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
`max_data_item_count` |
`int`
Max number of human labeled DataItems. This field is a member of `oneof` _ `human_labeling_budget` .
|
`max_data_item_percentage` |
`int`
Max percent of total DataItems for human labeling. This field is a member of `oneof` _ `human_labeling_budget` .
|
`sample_config` |
Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy. |
`training_config` |
CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems. |

## Methods

### ActiveLearningConfig

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PSCAutomationConfig -->

# Class PSCAutomationConfig (1.134.0)

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project id used to create forwarding rule. |
`network` |
`str`
Required. The full name of the Google Compute Engine `network ` __.
`Format ` __:
`projects/{project}/global/networks/{network}` .
|
`ip_address` |
`str`
Output only. IP address rule created by the PSC service automation. |
`forwarding_rule` |
`str`
Output only. Forwarding rule created by the PSC service automation. |
`state` |
Output only. The state of the PSC service automation. |
`error_message` |
`str`
Output only. Error message if the PSC service automation failed. |

## Methods

### PSCAutomationConfig

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeRequest -->

# Class AssignNotebookRuntimeRequest (1.134.0)

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to get the NotebookRuntime assignment. Format: `projects/{project}/locations/{location}`
|
`notebook_runtime_template` |
`str`
Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one). |
`notebook_runtime` |
Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. |
`notebook_runtime_id` |
`str`
Optional. User specified ID for the notebook runtime. |

## Methods

### AssignNotebookRuntimeRequest

```
AssignNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.AssignNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.DeployConfig.SystemLabelsEntry -->

# Class SystemLabelsEntry (1.134.0)

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.DataItemLabelsEntry -->

# Class DataItemLabelsEntry (1.134.0)

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

### DataItemLabelsEntry

`DataItemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRequest -->

# Class UpdateTensorboardRequest (1.134.0)

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the Tensorboard resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard` |
Required. The Tensorboard's `name` field is used to
identify the Tensorboard to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### UpdateTensorboardRequest

`UpdateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult -->

# Class LogprobsResult (1.134.0)

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

## Attributes |
|
|---|---|
Name |
Description |
`top_candidates` |
`MutableSequence[`
Length = total number of decoding steps. |
`chosen_candidates` |
`MutableSequence[`
Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates. |

## Classes

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidate for the logprobs token and score.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TopCandidates

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.

## Methods

### LogprobsResult

`LogprobsResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Logprobs Result

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardExperimentRequest -->

# Class CreateTensorboardExperimentRequest (1.134.0)

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`tensorboard_experiment` |
The TensorboardExperiment to create. |
`tensorboard_experiment_id` |
`str`
Required. The ID to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreateTensorboardExperimentRequest

```
CreateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.CreateTensorboardExperiment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceInput -->

# Class CoherenceInput (1.134.0)

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for coherence score metric. |
`instance` |
Required. Coherence instance. |

## Methods

### CoherenceInput

`CoherenceInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for coherence metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeResponse -->

# Class UpgradeNotebookRuntimeResponse (1.134.0)

```
UpgradeNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.UpgradeNotebookRuntime.

## Methods

### UpgradeNotebookRuntimeResponse

```
UpgradeNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.UpgradeNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ActiveLearningConfig -->

# Class ActiveLearningConfig (1.134.0)

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

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
`max_data_item_count` |
`int`
Max number of human labeled DataItems. This field is a member of `oneof` _ `human_labeling_budget` .
|
`max_data_item_percentage` |
`int`
Max percent of total DataItems for human labeling. This field is a member of `oneof` _ `human_labeling_budget` .
|
`sample_config` |
Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy. |
`training_config` |
CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems. |

## Methods

### ActiveLearningConfig

`ActiveLearningConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that configure the active learning pipeline. Active learning will label the data incrementally by several iterations. For every iteration, it will select a batch of data based on the sampling strategy.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest -->

# Class SearchNearestEntitiesRequest (1.134.0)

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`query` |
Required. The query. |
`return_full_entity` |
`bool`
Optional. If set to true, the full entities (including all vector values and metadata) of the nearest neighbors are returned; otherwise only entity id of the nearest neighbors will be returned. Note that returning full entities will significantly increase the latency and cost of the query. |

## Methods

### SearchNearestEntitiesRequest

```
SearchNearestEntitiesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The request message for FeatureOnlineStoreService.SearchNearestEntities.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresRequest -->

# Class ListMetadataStoresRequest (1.134.0)

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Location whose MetadataStores should be listed. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of Metadata Stores to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListMetadataStores call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |

## Methods

### ListMetadataStoresRequest

`ListMetadataStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataStores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RaySpec -->

# Class RaySpec (1.134.0)

`RaySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Optional. Default image for user to choose a preferred ML framework (for example, TensorFlow or Pytorch) by choosing from `Vertex prebuilt images |
`nfs_mounts` |
`MutableSequence[`
Optional. Use if you want to mount to any NFS storages. |
`resource_pool_images` |
`MutableMapping[str, str]`
Optional. Required if image_uri isn't set. A map of resource_pool_id to prebuild Ray image if user need to use different images for different head/worker pools. This map needs to cover all the resource pool ids. Example: { "ray_head_node_pool": "head image" "ray_worker_node_pool1": "worker image" "ray_worker_node_pool2": "another worker image" } |
`head_node_resource_pool_id` |
`str`
Optional. This will be used to indicate which resource pool will serve as the Ray head node(the first node within that pool). Will use the machine from the first workerpool as the head node by default if this field isn't set. |
`ray_metric_spec` |
Optional. Ray metrics configurations. |
`ray_logs_spec` |
Optional. OSS Ray logging configurations. |

## Classes

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### RaySpec

`RaySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentInstance -->

# Class FulfillmentInstance (1.134.0)

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

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
`instruction` |
`str`
Required. Inference instruction prompt to compare prediction with. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### FulfillmentInstance

`FulfillmentInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceResult -->

# Class CoherenceResult (1.134.0)

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Coherence score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for coherence score. |
`confidence` |
`float`
Output only. Confidence for coherence score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### CoherenceResult

`CoherenceResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EntityIdSelector -->

# Class EntityIdSelector (1.134.0)

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`csv_source` |
Source of Csv This field is a member of `oneof` _ `EntityIdsSource` .
|
`entity_id_field` |
`str`
Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity_id. |

## Methods

### EntityIdSelector

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageClassificationPredictionInstance -->

# Class ImageClassificationPredictionInstance (1.134.0)

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes or Cloud Storage URI to make the prediction on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## Methods

### ImageClassificationPredictionInstance

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

### ImageClassificationPredictionInstance

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxResult -->

# Class MetricxResult (1.134.0)

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. MetricX score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### MetricxResult

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.ManualRoutingMode -->

# Class ManualRoutingMode (1.134.0)

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
The model name to use. Only the public LLM models are accepted. e.g. 'gemini-1.5-pro-001'. This field is a member of `oneof` _ `_model_name` .
|

## Methods

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchResults -->

# Class ExactMatchResults (1.134.0)

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

## Attribute |
|
|---|---|
Name |
Description |
`exact_match_metric_values` |
`MutableSequence[`
Output only. Exact match metric values. |

## Methods

### ExactMatchResults

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoHyperParameters.TuningTask -->

# Class TuningTask (1.134.0)

`TuningTask(value)`


An enum defining the tuning task used for Veo.

## Enums |
|
|---|---|
Name |
Description |
`TUNING_TASK_UNSPECIFIED` |
Default value. This value is unused. |
`TUNING_TASK_I2V` |
Tuning task for image to video. |
`TUNING_TASK_T2V` |
Tuning task for text to video. |

## Methods

### TuningTask

`TuningTask(value)`


An enum defining the tuning task used for Veo.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest -->

# Class CreateFeatureMonitorRequest (1.134.0)

`CreateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][].

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of FeatureGroup to create FeatureMonitor. Format: `projects/{project}/locations/{location}/featureGroups/{featuregroup}`
|
`feature_monitor` |
Required. The Monitor to create. |
`feature_monitor_id` |
`str`
Required. The ID to use for this FeatureMonitor, which will become the final component of the FeatureGroup's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within the FeatureGroup.
|

## Methods

### CreateFeatureMonitorRequest

`CreateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][].

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient -->

# Class GenAiTuningServiceClient (1.134.0)

```
GenAiTuningServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing GenAI Tuning Jobs.

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
`GenAiTuningServiceTransport` |
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

### GenAiTuningServiceClient

```
GenAiTuningServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai tuning service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,GenAiTuningServiceTransport,Callable[..., GenAiTuningServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiTuningServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### cancel_tuning_job

```
cancel_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.CancelTuningJobRequest,
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
) -> None
```


Cancels a TuningJob. Starts asynchronous cancellation on the
TuningJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_GenAiTuningService.GetTuningJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the TuningJob is not deleted; instead it becomes a
job with a
xref_TuningJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_TuningJob.state is
set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_cancel_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTuningJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_cancel_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CancelTuningJob. |
`name` |
`str`
Required. The name of the TuningJob to cancel. Format: |
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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_tuning_job

```
create_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.CreateTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuning_job: typing.Optional[
google.cloud.aiplatform_v1.types.tuning_job.TuningJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tuning_job.TuningJob
```


Creates a TuningJob. A created TuningJob right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuning_job = aiplatform_v1.[TuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob.html)()
tuning_job.base_model = "base_model_value"
tuning_job.supervised_tuning_spec.training_dataset_uri = "training_dataset_uri_value"
request = aiplatform_v1.[CreateTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTuningJobRequest.html)(
parent="parent_value",
tuning_job=tuning_job,
)
# Make the request
response = client.[create_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_create_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CreateTuningJob. |
`parent` |
`str`
Required. The resource name of the Location to create the TuningJob in. Format: |
`tuning_job` |
Required. The TuningJob to create. This corresponds to the |
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
Represents a TuningJob that runs with Google owned models. |

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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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

### get_tuning_job

```
get_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.GetTuningJobRequest,
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
) -> google.cloud.aiplatform_v1.types.tuning_job.TuningJob
```


Gets a TuningJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_get_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.GetTuningJob. |
`name` |
`str`
Required. The name of the TuningJob resource. Format: |
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
Represents a TuningJob that runs with Google owned models. |

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

### list_tuning_jobs

```
list_tuning_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
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
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager
)
```


Lists TuningJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_tuning_jobs():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_list_tuning_jobs)(request=request)
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
The request object. Request message for GenAiTuningService.ListTuningJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the TuningJobs from. Format: |
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
Response message for GenAiTuningService.ListTuningJobs Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_tuning_job_path

`parse_tuning_job_path(path: str) -> typing.Dict[str, str]`


Parses a tuning_job path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### rebase_tuned_model

```
rebase_tuned_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.genai_tuning_service.RebaseTunedModelRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuned_model_ref: typing.Optional[
google.cloud.aiplatform_v1.types.tuning_job.TunedModelRef
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


Rebase a TunedModel.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_rebase_tuned_model():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuned_model_ref = aiplatform_v1.[TunedModelRef](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TunedModelRef.html)()
tuned_model_ref.tuned_model = "tuned_model_value"
request = aiplatform_v1.[RebaseTunedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebaseTunedModelRequest.html)(
parent="parent_value",
tuned_model_ref=tuned_model_ref,
)
# Make the request
operation = client.[rebase_tuned_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceClient_rebase_tuned_model)(request=request)
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
The request object. Request message for GenAiTuningService.RebaseTunedModel. |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: |
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. This corresponds to the |
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

### tuning_job_path

`tuning_job_path(project: str, location: str, tuning_job: str) -> str`


Returns a fully-qualified tuning_job string.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient -->

# Class FeatureOnlineStoreServiceClient (1.134.0)

```
FeatureOnlineStoreServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
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
google.cloud.aiplatform_v1beta1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDirectWriteRequest
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDirectWriteResponse
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
from google.cloud import aiplatform_v1beta1
def sample_feature_view_direct_write():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FeatureViewDirectWriteRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest.html)(
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.FeatureViewDirectWriteRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[feature_view_direct_write](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_feature_view_direct_write)(requests=request_generator())
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FetchFeatureValuesRequest,
dict,
]
] = None,
*,
feature_view: typing.Optional[str] = None,
data_key: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDataKey
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FetchFeatureValuesResponse
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
from google.cloud import aiplatform_v1beta1
def sample_fetch_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest.html)(
id="id_value",
feature_view="feature_view_value",
)
# Make the request
response = client.[fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_fetch_feature_values)(request=request)
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.GenerateFetchAccessTokenRequest,
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.GenerateFetchAccessTokenResponse
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
from google.cloud import aiplatform_v1beta1
def sample_generate_fetch_access_token():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GenerateFetchAccessTokenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest.html)(
)
# Make the request
response = client.[generate_fetch_access_token](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_generate_fetch_access_token)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][]. |
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
Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][]. |

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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.SearchNearestEntitiesRequest,
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.SearchNearestEntitiesResponse
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
from google.cloud import aiplatform_v1beta1
def sample_search_nearest_entities():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[NearestNeighborQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.html)()
query.entity_id = "entity_id_value"
request = aiplatform_v1beta1.[SearchNearestEntitiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest.html)(
feature_view="feature_view_value",
query=query,
)
# Make the request
response = client.[search_nearest_entities](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_search_nearest_entities)(request=request)
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

### streaming_fetch_feature_values

```
streaming_fetch_feature_values(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.StreamingFetchFeatureValuesRequest
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
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.StreamingFetchFeatureValuesResponse
]
```


Bidirectional streaming RPC to fetch feature values under a FeatureView. Requests may not have a one-to-one mapping to responses and responses may be returned out-of-order to reduce latency.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_streaming_fetch_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingFetchFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingFetchFeatureValuesRequest.html)(
feature_view="feature_view_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamingFetchFeatureValuesRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[streaming_fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_streaming_fetch_feature_values)(requests=request_generator())
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
The request object iterator. Request message for FeatureOnlineStoreService.StreamingFetchFeatureValues. For the entities requested, all features under the requested feature view will be returned. |
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
Response message for FeatureOnlineStoreService.StreamingFetchFeatureValues. |

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
