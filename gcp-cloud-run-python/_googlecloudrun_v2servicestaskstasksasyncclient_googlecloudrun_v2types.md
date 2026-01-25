---
merged_at: 2026-01-25T12:06:29.188034
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicestaskstasksasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.TasksAsyncClient -->

# Class TasksAsyncClient (0.14.0)

```
TasksAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.tasks.transports.base.TasksTransport,
typing.Callable[
[...], google.cloud.run_v2.services.tasks.transports.base.TasksTransport
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Cloud Run Task Control Plane API.

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
`TasksTransport` |
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

### TasksAsyncClient

```
TasksAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.tasks.transports.base.TasksTransport,
typing.Callable[
[...], google.cloud.run_v2.services.tasks.transports.base.TasksTransport
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the tasks async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,TasksTransport,Callable[..., TasksTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the TasksTransport constructor. If set to None, a transport is chosen automatically. |
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

### connector_path

`connector_path(project: str, location: str, connector: str) -> str`


Returns a fully-qualified connector string.

### crypto_key_path

`crypto_key_path(project: str, location: str, key_ring: str, crypto_key: str) -> str`


Returns a fully-qualified crypto_key string.

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

`execution_path(project: str, location: str, job: str, execution: str) -> str`


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
`TasksAsyncClient` |
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
`TasksAsyncClient` |
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
`TasksAsyncClient` |
The constructed client. |

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

### get_task

```
get_task(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.task.GetTaskRequest, dict]
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
) -> google.cloud.run_v2.types.task.Task
```


Gets information about a Task.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import
```[run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest)
async def sample_get_task():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[TasksAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.TasksAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[GetTaskRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetTaskRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_task](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.TasksAsyncClient.html#google_cloud_run_v2_services_tasks_TasksAsyncClient_get_task)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for obtaining a Task by its full name. |
`name` |
Required. The full name of the Task. Format: projects/{project}/locations/{location}/jobs/{job}/executions/{execution}/tasks/{task} This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Task represents a single run of a container to completion. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[google.cloud.run_v2.services.tasks.transports.base.TasksTransport]
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

### job_path

`job_path(project: str, location: str, job: str) -> str`


Returns a fully-qualified job string.

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

### list_tasks

```
list_tasks(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.task.ListTasksRequest, dict]
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
) -> google.cloud.run_v2.services.tasks.pagers.ListTasksAsyncPager
```


Lists Tasks from an Execution of a Job.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import
```[run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest)
async def sample_list_tasks():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[TasksAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.TasksAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ListTasksRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tasks](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.TasksAsyncClient.html#google_cloud_run_v2_services_tasks_TasksAsyncClient_list_tasks)(request=request)
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
The request object. Request message for retrieving a list of Tasks. |
`parent` |
Required. The Execution from which the Tasks should be listed. To list all Tasks across Executions of a Job, use "-" instead of Execution name. To list all Tasks across Jobs, use "-" instead of Job name. Format: projects/{project}/locations/{location}/jobs/{job}/executions/{execution} This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message containing a list of Tasks. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_connector_path

`parse_connector_path(path: str) -> typing.Dict[str, str]`


Parses a connector path into its component segments.

### parse_crypto_key_path

`parse_crypto_key_path(path: str) -> typing.Dict[str, str]`


Parses a crypto_key path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_job_path

`parse_job_path(path: str) -> typing.Dict[str, str]`


Parses a job path into its component segments.

### parse_secret_path

`parse_secret_path(path: str) -> typing.Dict[str, str]`


Parses a secret path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### parse_task_path

`parse_task_path(path: str) -> typing.Dict[str, str]`


Parses a task path into its component segments.

### secret_path

`secret_path(project: str, secret: str) -> str`


Returns a fully-qualified secret string.

### secret_version_path

`secret_version_path(project: str, secret: str, version: str) -> str`


Returns a fully-qualified secret_version string.

### task_path

`task_path(project: str, location: str, job: str, execution: str, task: str) -> str`


Returns a fully-qualified task string.

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types -->

# Package types (0.14.0)

API documentation for `run_v2.types`

package.

## Classes

[BinaryAuthorization](/python/docs/reference/run/latest/google.cloud.run_v2.types.BinaryAuthorization)

Settings for Binary Authorization feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[BuildConfig](/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig)

Describes the Build step of the function that builds a container from the given source.

[BuildInfo](/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildInfo)

Build information of the image.

[CancelExecutionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CancelExecutionRequest)

Request message for deleting an Execution.

[CloudSqlInstance](/python/docs/reference/run/latest/google.cloud.run_v2.types.CloudSqlInstance)

Represents a set of Cloud SQL instances. Each one will be available
under /cloudsql/[instance]. Visit
[https://cloud.google.com/sql/docs/mysql/connect-run](https://cloud.google.com/sql/docs/mysql/connect-run) for more
information on how to connect Cloud SQL and Cloud Run.

[Condition](/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition)

Defines a status condition for a resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Container](/python/docs/reference/run/latest/google.cloud.run_v2.types.Container)

A single application container. This specifies both the container to run, the command to run in the container and the arguments to supply to it. Note that additional arguments can be supplied by the system to the container at runtime.

[ContainerPort](/python/docs/reference/run/latest/google.cloud.run_v2.types.ContainerPort)

ContainerPort represents a network port in a single container.

[CreateJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateJobRequest)

Request message for creating a Job.

[CreateServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateServiceRequest)

Request message for creating a Service.

[CreateWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateWorkerPoolRequest)

Request message for creating a WorkerPool.

[DeleteExecutionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteExecutionRequest)

Request message for deleting an Execution.

[DeleteJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteJobRequest)

Request message to delete a Job by its full name.

[DeleteRevisionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteRevisionRequest)

Request message for deleting a retired Revision. Revision lifecycle is usually managed by making changes to the parent Service. Only retired revisions can be deleted with this API.

[DeleteServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteServiceRequest)

Request message to delete a Service by its full name.

[DeleteWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteWorkerPoolRequest)

Request message to delete a WorkerPool by its full name.

[EmptyDirVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource)

In memory (tmpfs) ephemeral storage. It is ephemeral in the sense that when the sandbox is taken down, the data is destroyed with it (it does not persist across sandbox runs).

[EncryptionKeyRevocationAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.EncryptionKeyRevocationAction)

Specifies behavior if an encryption key used by a resource is revoked.

[EnvVar](/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVar)

EnvVar represents an environment variable present in a Container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EnvVarSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVarSource)

EnvVarSource represents a source for the value of an EnvVar.

[Execution](/python/docs/reference/run/latest/google.cloud.run_v2.types.Execution)

Execution represents the configuration of a single execution. A execution an immutable resource that references a container image which is run to completion.

[ExecutionEnvironment](/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionEnvironment)

Alternatives for execution environments.

[ExecutionReference](/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionReference)

Reference to an Execution. Use /Executions.GetExecution with the given name to get full execution including the latest status.

[ExecutionTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionTemplate)

ExecutionTemplate describes the data an execution should have when created from a template.

[GCSVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.GCSVolumeSource)

Represents a volume backed by a Cloud Storage bucket using Cloud Storage FUSE.

[GRPCAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.GRPCAction)

GRPCAction describes an action involving a GRPC port.

[GetExecutionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetExecutionRequest)

Request message for obtaining a Execution by its full name.

[GetJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetJobRequest)

Request message for obtaining a Job by its full name.

[GetRevisionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetRevisionRequest)

Request message for obtaining a Revision by its full name.

[GetServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetServiceRequest)

Request message for obtaining a Service by its full name.

[GetTaskRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetTaskRequest)

Request message for obtaining a Task by its full name.

[GetWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetWorkerPoolRequest)

Request message for obtaining a WorkerPool by its full name.

[HTTPGetAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPGetAction)

HTTPGetAction describes an action based on HTTP Get requests.

[HTTPHeader](/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPHeader)

HTTPHeader describes a custom header to be used in HTTP probes

[IngressTraffic](/python/docs/reference/run/latest/google.cloud.run_v2.types.IngressTraffic)

Allowed ingress traffic for the Container.

[InstanceSplit](/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplit)

Holds a single instance split entry for the Worker. Allocations can be done to a specific Revision name, or pointing to the latest Ready Revision.

[InstanceSplitAllocationType](/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitAllocationType)

The type of instance split allocation.

[InstanceSplitStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitStatus)

Represents the observed state of a single `InstanceSplit`

entry.

[Job](/python/docs/reference/run/latest/google.cloud.run_v2.types.Job)

Job represents the configuration of a single job, which references a container image that is run to completion.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ListExecutionsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsRequest)

Request message for retrieving a list of Executions.

[ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse)

Response message containing a list of Executions.

[ListJobsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsRequest)

Request message for retrieving a list of Jobs.

[ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse)

Response message containing a list of Jobs.

[ListRevisionsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsRequest)

Request message for retrieving a list of Revisions.

[ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse)

Response message containing a list of Revisions.

[ListServicesRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesRequest)

Request message for retrieving a list of Services.

[ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse)

Response message containing a list of Services.

[ListTasksRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksRequest)

Request message for retrieving a list of Tasks.

[ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse)

Response message containing a list of Tasks.

[ListWorkerPoolsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsRequest)

Request message for retrieving a list of WorkerPools.

[ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse)

Response message containing a list of WorkerPools.

[NFSVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.NFSVolumeSource)

Represents an NFS mount.

[NodeSelector](/python/docs/reference/run/latest/google.cloud.run_v2.types.NodeSelector)

Hardware constraints configuration.

[Probe](/python/docs/reference/run/latest/google.cloud.run_v2.types.Probe)

Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ResourceRequirements](/python/docs/reference/run/latest/google.cloud.run_v2.types.ResourceRequirements)

ResourceRequirements describes the compute resource requirements.

[Revision](/python/docs/reference/run/latest/google.cloud.run_v2.types.Revision)

A Revision is an immutable snapshot of code and configuration. A Revision references a container image. Revisions are only created by updates to its parent Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RevisionScaling](/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScaling)

Settings for revision-level scaling settings.

[RevisionScalingStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScalingStatus)

Effective settings for the current revision

[RevisionTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionTemplate)

RevisionTemplate describes the data a revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RunJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest)

Request message to create a new Execution of a Job.

[SecretKeySelector](/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretKeySelector)

SecretEnvVarSource represents a source for the value of an EnvVar.

[SecretVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretVolumeSource)

The secret's value will be presented as the content of a file whose name is defined in the item path. If no items are defined, the name of the file is the secret.

[Service](/python/docs/reference/run/latest/google.cloud.run_v2.types.Service)

Service acts as a top-level container that manages a set of configurations and revision templates which implement a network service. Service exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership.

[ServiceMesh](/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceMesh)

Settings for Cloud Service Mesh. For more information see
[https://cloud.google.com/service-mesh/docs/overview](https://cloud.google.com/service-mesh/docs/overview).

[ServiceScaling](/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling)

Scaling settings applied at the service level rather than at the revision level.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SourceCode](/python/docs/reference/run/latest/google.cloud.run_v2.types.SourceCode)

Source type for the container.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StorageSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.StorageSource)

Location of the source in an archive file in Google Cloud Storage.

[SubmitBuildRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest)

Request message for submitting a Build.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SubmitBuildResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildResponse)

Response message for submitting a Build.

[TCPSocketAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.TCPSocketAction)

TCPSocketAction describes an action based on opening a socket

[Task](/python/docs/reference/run/latest/google.cloud.run_v2.types.Task)

Task represents a single run of a container to completion.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TaskAttemptResult](/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskAttemptResult)

Result of a task attempt.

[TaskTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskTemplate)

TaskTemplate describes the data a task should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrafficTarget](/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTarget)

Holds a single traffic routing entry for the Service. Allocations can be done to a specific Revision name, or pointing to the latest Ready Revision.

[TrafficTargetAllocationType](/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetAllocationType)

The type of instance allocation.

[TrafficTargetStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetStatus)

Represents the observed state of a single `TrafficTarget`

entry.

[UpdateJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateJobRequest)

Request message for updating a Job.

[UpdateServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateServiceRequest)

Request message for updating a service.

[UpdateWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateWorkerPoolRequest)

Request message for updating a worker pool.

[VersionToPath](/python/docs/reference/run/latest/google.cloud.run_v2.types.VersionToPath)

VersionToPath maps a specific version of a secret to a relative file to mount to, relative to VolumeMount's mount_path.

[Volume](/python/docs/reference/run/latest/google.cloud.run_v2.types.Volume)

Volume represents a named volume in a container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[VolumeMount](/python/docs/reference/run/latest/google.cloud.run_v2.types.VolumeMount)

VolumeMount describes a mounting of a Volume within a container.

[VpcAccess](/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess)

VPC Access settings. For more information on sending traffic
to a VPC network, visit
[https://cloud.google.com/run/docs/configuring/connecting-vpc](https://cloud.google.com/run/docs/configuring/connecting-vpc).

[WorkerPool](/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPool)

WorkerPool acts as a top-level container that manages a set of configurations and revision templates which implement a pull-based workload. WorkerPool exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership.

[WorkerPoolRevisionTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolRevisionTemplate)

WorkerPoolRevisionTemplate describes the data a worker pool revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[WorkerPoolScaling](/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolScaling)

Worker pool scaling settings.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)
