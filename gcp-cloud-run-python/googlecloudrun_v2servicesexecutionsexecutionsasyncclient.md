---
source_url: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient
fetched_at: 2026-02-09T09:25:22.074295
---

# Class ExecutionsAsyncClient (0.15.0)

```
ExecutionsAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.executions.transports.base.ExecutionsTransport,
typing.Callable[
[...],
google.cloud.run_v2.services.executions.transports.base.ExecutionsTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Cloud Run Execution Control Plane API.

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
`ExecutionsTransport` |
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

### ExecutionsAsyncClient

```
ExecutionsAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.executions.transports.base.ExecutionsTransport,
typing.Callable[
[...],
google.cloud.run_v2.services.executions.transports.base.ExecutionsTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the executions async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ExecutionsTransport,Callable[..., ExecutionsTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ExecutionsTransport constructor. If set to None, a transport is chosen automatically. |
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

### cancel_execution

```
cancel_execution(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.execution.CancelExecutionRequest, dict]
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


Cancels an Execution.

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
async def sample_cancel_execution():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ExecutionsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[CancelExecutionRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CancelExecutionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[cancel_execution](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html#google_cloud_run_v2_services_executions_ExecutionsAsyncClient_cancel_execution)(request=request)
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
The request object. Request message for deleting an Execution. |
`name` |
Required. The name of the Execution to cancel. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_execution

```
delete_execution(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.execution.DeleteExecutionRequest, dict]
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
from google.cloud import
```[run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest)
async def sample_delete_execution():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ExecutionsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[DeleteExecutionRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteExecutionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_execution](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html#google_cloud_run_v2_services_executions_ExecutionsAsyncClient_delete_execution)(request=request)
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
The request object. Request message for deleting an Execution. |
`name` |
Required. The name of the Execution to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ExecutionsAsyncClient` |
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
`ExecutionsAsyncClient` |
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
`ExecutionsAsyncClient` |
The constructed client. |

### get_execution

```
get_execution(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.execution.GetExecutionRequest, dict]
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
) -> google.cloud.run_v2.types.execution.Execution
```


Gets information about an Execution.

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
async def sample_get_execution():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ExecutionsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[GetExecutionRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetExecutionRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_execution](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html#google_cloud_run_v2_services_executions_ExecutionsAsyncClient_get_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for obtaining a Execution by its full name. |
`name` |
Required. The full name of the Execution. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Execution represents the configuration of a single execution. A execution an immutable resource that references a container image which is run to completion. |

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
google.cloud.run_v2.services.executions.transports.base.ExecutionsTransport
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

### job_path

`job_path(project: str, location: str, job: str) -> str`


Returns a fully-qualified job string.

### list_executions

```
list_executions(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.execution.ListExecutionsRequest, dict]
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
) -> google.cloud.run_v2.services.executions.pagers.ListExecutionsAsyncPager
```


Lists Executions from a Job. Results are sorted by creation time, descending.

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
async def sample_list_executions():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ExecutionsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ListExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_executions](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.ExecutionsAsyncClient.html#google_cloud_run_v2_services_executions_ExecutionsAsyncClient_list_executions)(request=request)
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
The request object. Request message for retrieving a list of Executions. |
`parent` |
Required. The Execution from which the Executions should be listed. To list all Executions across Jobs, use "-" instead of Job name. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message containing a list of Executions. Iterating over this object will yield results and resolve additional pages automatically. |

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

### secret_path

`secret_path(project: str, secret: str) -> str`


Returns a fully-qualified secret string.

### secret_version_path

`secret_version_path(project: str, secret: str, version: str) -> str`


Returns a fully-qualified secret_version string.

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