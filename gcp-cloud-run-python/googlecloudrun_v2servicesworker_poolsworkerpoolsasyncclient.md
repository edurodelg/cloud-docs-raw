---
source_url: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient
fetched_at: 2026-01-28T07:18:54.628437
---

# Class WorkerPoolsAsyncClient (0.14.0)

```
WorkerPoolsAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.worker_pools.transports.base.WorkerPoolsTransport,
typing.Callable[
[...],
google.cloud.run_v2.services.worker_pools.transports.base.WorkerPoolsTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Cloud Run WorkerPool Control Plane API.

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
`WorkerPoolsTransport` |
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

### WorkerPoolsAsyncClient

```
WorkerPoolsAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.worker_pools.transports.base.WorkerPoolsTransport,
typing.Callable[
[...],
google.cloud.run_v2.services.worker_pools.transports.base.WorkerPoolsTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the worker pools async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,WorkerPoolsTransport,Callable[..., WorkerPoolsTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the WorkerPoolsTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_worker_pool

```
create_worker_pool(
request: typing.Optional[
typing.Union[
google.cloud.run_v2.types.worker_pool.CreateWorkerPoolRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
worker_pool: typing.Optional[
google.cloud.run_v2.types.worker_pool.WorkerPool
] = None,
worker_pool_id: typing.Optional[str] = None,
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


Creates a new WorkerPool in a given project and location.

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
async def sample_create_worker_pool():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[CreateWorkerPoolRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateWorkerPoolRequest.html)(
parent="parent_value",
worker_pool_id="worker_pool_id_value",
)
# Make the request
operation = client.[create_worker_pool](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_create_worker_pool)(request=request)
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
The request object. Request message for creating a WorkerPool. |
`parent` |
Required. The location and project in which this worker pool should be created. Format: |
`worker_pool` |
Required. The WorkerPool instance to create. This corresponds to the |
`worker_pool_id` |
Required. The unique identifier for the WorkerPool. It must begin with letter, and cannot end with hyphen; must contain fewer than 50 characters. The name of the worker pool becomes |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_worker_pool

```
delete_worker_pool(
request: typing.Optional[
typing.Union[
google.cloud.run_v2.types.worker_pool.DeleteWorkerPoolRequest, dict
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


Deletes a WorkerPool.

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
async def sample_delete_worker_pool():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[DeleteWorkerPoolRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteWorkerPoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_worker_pool](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_delete_worker_pool)(request=request)
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
The request object. Request message to delete a WorkerPool by its full name. |
`name` |
Required. The full name of the WorkerPool. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`WorkerPoolsAsyncClient` |
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
`WorkerPoolsAsyncClient` |
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
`WorkerPoolsAsyncClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[
typing.Union[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest, dict]
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
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM Access Control policy currently in effect for the given Cloud Run WorkerPool. This result does not include any inherited policies.

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
from google.iam.v1 import iam_policy_pb2 # type: ignore
async def sample_get_iam_policy():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = iam_policy_pb2.GetIamPolicyRequest(
resource="resource_value",
)
# Make the request
response = await client.[get_iam_policy](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_get_iam_policy)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
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
`google.iam.v1.policy_pb2.Policy` |
An Identity and Access Management (IAM) policy, which specifies access controls for Google Cloud resources. A Policy is a collection of bindings. A binding binds one or more members, or principals, to a single role. Principals can be user accounts, service accounts, Google groups, and domains (such as G Suite). A role is a named list of permissions; each role can be an IAM predefined role or a user-created custom role. For some types of Google Cloud resources, a binding can also specify a condition, which is a logical expression that allows access to a resource only if the expression evaluates to true. A condition can add constraints based on attributes of the request, the resource, or both. To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies). **JSON example:** :literal:` { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": [ "user:eve@example.com" ], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ],="" "etag":="" "bwwwja0yfja=", " version":="" 3="">` \ \` **YAML example:** :literal:` bindings: - members: - user:mike@example.com - group:admins@example.com - domain:google.com - serviceAccount:my-project-id@appspot.gserviceaccount.com role: roles/resourcemanager.organizationAdmin - members: - user:eve@example.com role: roles/resourcemanager.organizationViewer condition: title: expirable access description: Does not grant access after Sep 2020 expression: request.time < timestamp('2020-10-01t00:00:00.000z')="" etag:="" bwwwja0yfja="version:">`\ \` For a description of IAM and its features, see the [IAM documentation](https://cloud.google.com/iam/docs/). |

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
google.cloud.run_v2.services.worker_pools.transports.base.WorkerPoolsTransport
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

### get_worker_pool

```
get_worker_pool(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.worker_pool.GetWorkerPoolRequest, dict]
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
) -> google.cloud.run_v2.types.worker_pool.WorkerPool
```


Gets information about a WorkerPool.

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
async def sample_get_worker_pool():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[GetWorkerPoolRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetWorkerPoolRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_worker_pool](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_get_worker_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for obtaining a WorkerPool by its full name. |
`name` |
Required. The full name of the WorkerPool. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
WorkerPool acts as a top-level container that manages a set of configurations and revision templates which implement a pull-based workload. WorkerPool exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership. |

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

### list_worker_pools

```
list_worker_pools(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest, dict]
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
) -> google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsAsyncPager
```


Lists WorkerPools. Results are sorted by creation time, descending.

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
async def sample_list_worker_pools():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ListWorkerPoolsRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_worker_pools](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_list_worker_pools)(request=request)
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
The request object. Request message for retrieving a list of WorkerPools. |
`parent` |
Required. The location and project to list resources on. Location must be a valid Google Cloud region, and cannot be the "-" wildcard. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message containing a list of WorkerPools. Iterating over this object will yield results and resolve additional pages automatically. |

### mesh_path

`mesh_path(project: str, location: str, mesh: str) -> str`


Returns a fully-qualified mesh string.

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

### parse_mesh_path

`parse_mesh_path(path: str) -> typing.Dict[str, str]`


Parses a mesh path into its component segments.

### parse_policy_path

`parse_policy_path(path: str) -> typing.Dict[str, str]`


Parses a policy path into its component segments.

### parse_revision_path

`parse_revision_path(path: str) -> typing.Dict[str, str]`


Parses a revision path into its component segments.

### parse_secret_path

`parse_secret_path(path: str) -> typing.Dict[str, str]`


Parses a secret path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### parse_worker_pool_path

`parse_worker_pool_path(path: str) -> typing.Dict[str, str]`


Parses a worker_pool path into its component segments.

### policy_path

`policy_path(project: str) -> str`


Returns a fully-qualified policy string.

### revision_path

`revision_path(project: str, location: str, service: str, revision: str) -> str`


Returns a fully-qualified revision string.

### secret_path

`secret_path(project: str, secret: str) -> str`


Returns a fully-qualified secret string.

### secret_version_path

`secret_version_path(project: str, secret: str, version: str) -> str`


Returns a fully-qualified secret_version string.

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[
typing.Union[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest, dict]
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
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM Access control policy for the specified WorkerPool. Overwrites any existing policy.

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
from google.iam.v1 import iam_policy_pb2 # type: ignore
async def sample_set_iam_policy():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = iam_policy_pb2.SetIamPolicyRequest(
resource="resource_value",
)
# Make the request
response = await client.[set_iam_policy](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_set_iam_policy)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
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
`google.iam.v1.policy_pb2.Policy` |
An Identity and Access Management (IAM) policy, which specifies access controls for Google Cloud resources. A Policy is a collection of bindings. A binding binds one or more members, or principals, to a single role. Principals can be user accounts, service accounts, Google groups, and domains (such as G Suite). A role is a named list of permissions; each role can be an IAM predefined role or a user-created custom role. For some types of Google Cloud resources, a binding can also specify a condition, which is a logical expression that allows access to a resource only if the expression evaluates to true. A condition can add constraints based on attributes of the request, the resource, or both. To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies). **JSON example:** :literal:` { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": [ "user:eve@example.com" ], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ],="" "etag":="" "bwwwja0yfja=", " version":="" 3="">` \ \` **YAML example:** :literal:` bindings: - members: - user:mike@example.com - group:admins@example.com - domain:google.com - serviceAccount:my-project-id@appspot.gserviceaccount.com role: roles/resourcemanager.organizationAdmin - members: - user:eve@example.com role: roles/resourcemanager.organizationViewer condition: title: expirable access description: Does not grant access after Sep 2020 expression: request.time < timestamp('2020-10-01t00:00:00.000z')="" etag:="" bwwwja0yfja="version:">`\ \` For a description of IAM and its features, see the [IAM documentation](https://cloud.google.com/iam/docs/). |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
typing.Union[google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest, dict]
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


Returns permissions that a caller has on the specified Project. There are no permissions required for making this API call.

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
from google.iam.v1 import iam_policy_pb2 # type: ignore
async def sample_test_iam_permissions():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = iam_policy_pb2.TestIamPermissionsRequest(
resource="resource_value",
permissions=['permissions_value1', 'permissions_value2'],
)
# Make the request
response = await client.[test_iam_permissions](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_test_iam_permissions)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
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
Response message for TestIamPermissions method. |

### update_worker_pool

```
update_worker_pool(
request: typing.Optional[
typing.Union[
google.cloud.run_v2.types.worker_pool.UpdateWorkerPoolRequest, dict
]
] = None,
*,
worker_pool: typing.Optional[
google.cloud.run_v2.types.worker_pool.WorkerPool
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


Updates a WorkerPool.

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
async def sample_update_worker_pool():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[WorkerPoolsAsyncClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[UpdateWorkerPoolRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateWorkerPoolRequest.html)(
)
# Make the request
operation = client.[update_worker_pool](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.WorkerPoolsAsyncClient.html#google_cloud_run_v2_services_worker_pools_WorkerPoolsAsyncClient_update_worker_pool)(request=request)
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
The request object. Request message for updating a worker pool. |
`worker_pool` |
Required. The WorkerPool to be updated. This corresponds to the |
`update_mask` |
Optional. The list of fields to be updated. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### worker_pool_path

`worker_pool_path(project: str, location: str, worker_pool: str) -> str`


Returns a fully-qualified worker_pool string.