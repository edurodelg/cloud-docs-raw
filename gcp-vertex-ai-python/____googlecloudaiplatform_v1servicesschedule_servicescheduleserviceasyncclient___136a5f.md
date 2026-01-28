---
merged_at: 2026-01-28T15:11:44.798747
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient -->

# Class ScheduleServiceAsyncClient (1.135.0)

```
ScheduleServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

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
`ScheduleServiceTransport` |
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

### ScheduleServiceAsyncClient

```
ScheduleServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the schedule service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ScheduleServiceTransport,Callable[..., ScheduleServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ScheduleServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_schedule

```
create_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.CreateScheduleRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
schedule: typing.Optional[
google.cloud.aiplatform_v1.types.schedule.Schedule
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Creates a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1.[CreateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateScheduleRequest.html)(
parent="parent_value",
schedule=schedule,
)
# Make the request
response = await client.[create_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_create_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.CreateSchedule. |
`parent` |
Required. The resource name of the Location to create the Schedule in. Format: |
`schedule` |
Required. The Schedule to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

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

### delete_schedule

```
delete_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.DeleteScheduleRequest,
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


Deletes a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteScheduleRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_delete_schedule)(request=request)
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
The request object. Request message for ScheduleService.DeleteSchedule. |
`name` |
Required. The name of the Schedule resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ScheduleServiceAsyncClient` |
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
`ScheduleServiceAsyncClient` |
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
`ScheduleServiceAsyncClient` |
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

### get_schedule

```
get_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.GetScheduleRequest, dict
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
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Gets a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetScheduleRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_get_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.GetSchedule. |
`name` |
Required. The name of the Schedule resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport
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

### list_schedules

```
list_schedules(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest, dict
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
google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesAsyncPager
)
```


Lists Schedules in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_schedules():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSchedulesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_schedules](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_list_schedules)(request=request)
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
The request object. Request message for ScheduleService.ListSchedules. |
`parent` |
Required. The resource name of the Location to list the Schedules from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ScheduleService.ListSchedules Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

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

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### pause_schedule

```
pause_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.PauseScheduleRequest, dict
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


Pauses a Schedule. Will mark xref_Schedule.state to 'PAUSED'. If the schedule is paused, no new runs will be created. Already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_pause_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PauseScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseScheduleRequest.html)(
name="name_value",
)
# Make the request
await client.[pause_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_pause_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.PauseSchedule. |
`name` |
Required. The name of the Schedule resource to be paused. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_schedule

```
resume_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.ResumeScheduleRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
catch_up: typing.Optional[bool] = None,
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


Resumes a paused Schedule to start scheduling new runs. Will mark xref_Schedule.state to 'ACTIVE'. Only paused Schedule can be resumed.

When the Schedule is resumed, new runs will be scheduled starting from the next execution time after the current time based on the time_specification in the Schedule. If xref_Schedule.catch_up is set up true, all missed runs will be scheduled for backfill first.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_resume_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ResumeScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeScheduleRequest.html)(
name="name_value",
)
# Make the request
await client.[resume_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_resume_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.ResumeSchedule. |
`name` |
Required. The name of the Schedule resource to be resumed. Format: |
`catch_up` |
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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

### update_schedule

```
update_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.UpdateScheduleRequest,
dict,
]
] = None,
*,
schedule: typing.Optional[
google.cloud.aiplatform_v1.types.schedule.Schedule
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
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Updates an active or paused Schedule.

When the Schedule is updated, new runs will be scheduled starting from the updated next execution time after the update time based on the time_specification in the updated Schedule. All unstarted runs before the update time will be skipped while already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1.[UpdateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateScheduleRequest.html)(
schedule=schedule,
)
# Make the request
response = await client.[update_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_update_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.UpdateSchedule. |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. This corresponds to the |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsAsyncPager -->

# Class ListCustomJobsAsyncPager (1.135.0)

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCustomJobsAsyncPager

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEntityTypeRequest -->

# Class GetEntityTypeRequest (1.135.0)

`GetEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetEntityType.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the EntityType resource. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|

## Methods

### GetEntityTypeRequest

`GetEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetEntityType.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreOperationMetadata -->

# Class UpdateExampleStoreOperationMetadata (1.135.0)

```
UpdateExampleStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ExampleStoreService.UpdateExampleStore operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateExampleStoreOperationMetadata

```
UpdateExampleStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ExampleStoreService.UpdateExampleStore operation.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorOperationMetadata -->

# Class UpdateFeatureMonitorOperationMetadata (1.135.0)

```
UpdateFeatureMonitorOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update FeatureMonitor.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for FeatureMonitor. |

## Methods

### UpdateFeatureMonitorOperationMetadata

```
UpdateFeatureMonitorOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update FeatureMonitor.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse -->

# Class ListModelsResponse (1.135.0)

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModels

## Attributes |
|
|---|---|
Name |
Description |
`models` |
`MutableSequence[`
List of Models in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelsRequest.page_token to obtain that page. |

## Methods

### ListModelsResponse

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModels

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager -->

# Class ListRagFilesAsyncPager (1.135.0)

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagFilesAsyncPager

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExampleStoreOperationMetadata -->

# Class CreateExampleStoreOperationMetadata (1.135.0)

```
CreateExampleStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ExampleStoreService.CreateExampleStore operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### CreateExampleStoreOperationMetadata

```
CreateExampleStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ExampleStoreService.CreateExampleStore operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec.MultiTrialAlgorithmSpec.MetricSpec -->

# Class MetricSpec (1.135.0)

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

## Attributes |
|
|---|---|
Name |
Description |
`metric_id` |
`str`
Required. The ID of the metric. Must not contain whitespaces. |
`goal` |
Required. The optimization goal of the metric. |

## Classes

### GoalType

`GoalType(value)`


The available types of optimization goals.

## Methods

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesOperationMetadata -->

# Class DeleteFeatureValuesOperationMetadata (1.135.0)

```
DeleteFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that delete Feature values.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore delete Features values. |

## Methods

### DeleteFeatureValuesOperationMetadata

```
DeleteFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that delete Feature values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineResponse -->

# Class QueryReasoningEngineResponse (1.135.0)

```
QueryReasoningEngineResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ReasoningEngineExecutionService.Query][]

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`google.protobuf.struct_pb2.Value`
Response provided by users in JSON object format. |

## Methods

### QueryReasoningEngineResponse

```
QueryReasoningEngineResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ReasoningEngineExecutionService.Query][]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitorJob -->

# Class FeatureMonitorJob (1.135.0)

`FeatureMonitorJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Monitor Job.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. Name of the FeatureMonitorJob. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}/featureMonitorJobs/{feature_monitor_job}` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureMonitorJob was created. Creation of a FeatureMonitorJob means that the job is pending / waiting for sufficient resources but may not have started running yet. |
`final_status` |
`google.rpc.status_pb2.Status`
Output only. Final status of the FeatureMonitorJob. |
`job_summary` |
Output only. Summary from the FeatureMonitorJob. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureMonitorJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureMonitor(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`description` |
`str`
Optional. Description of the FeatureMonitor. |
`drift_base_feature_monitor_job_id` |
`int`
Output only. FeatureMonitorJob ID comparing to which the drift is calculated. |
`drift_base_snapshot_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Data snapshot time comparing to which the drift is calculated. |
`feature_selection_config` |
Output only. Feature selection config used when creating FeatureMonitorJob. |
`trigger_type` |
Output only. Trigger type of the Feature Monitor Job. |

## Classes

### FeatureMonitorJobTrigger

`FeatureMonitorJobTrigger(value)`


Choices of the trigger type.

### JobSummary

`JobSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the FeatureMonitorJob.

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

### FeatureMonitorJob

`FeatureMonitorJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Monitor Job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsPager -->

# Class ListNasTrialDetailsPager (1.135.0)

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
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


A pager for iterating through `list_nas_trial_details`

requests.

This class thinly wraps an initial
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_trial_details`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNasTrialDetails`

requests and continue to iterate
through the `nas_trial_details`

field on the
corresponding responses.

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasTrialDetailsPager

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityInstance -->

# Class SummarizationQualityInstance (1.135.0)

```
SummarizationQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization quality instance.

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
Required. Summarization prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### SummarizationQualityInstance

```
SummarizationQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexEndpointRequest -->

# Class GetIndexEndpointRequest (1.135.0)

`GetIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.GetIndexEndpoint

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the IndexEndpoint resource. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|

## Methods

### GetIndexEndpointRequest

`GetIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.GetIndexEndpoint

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LargeModelReference -->

# Class LargeModelReference (1.135.0)

`LargeModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the Large Model.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The unique name of the large Foundation or pre-built model. Like "chat-bison", "text-bison". Or model name with version ID, like "chat-bison@001", "text-bison@005", etc. |

## Methods

### LargeModelReference

`LargeModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the Large Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsPager -->

# Class ListExtensionsPager (1.135.0)

```
ListExtensionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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


A pager for iterating through `list_extensions`

requests.

This class thinly wraps an initial
[ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse) object, and
provides an `__iter__`

method to iterate through its
`extensions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExtensions`

requests and continue to iterate
through the `extensions`

field on the
corresponding responses.

All the usual [ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExtensionsPager

```
ListExtensionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagEngineConfigRequest -->

# Class GetRagEngineConfigRequest (1.135.0)

`GetRagEngineConfigRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagEngineConfig

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagEngineConfig resource. Format: `projects/{project}/locations/{location}/ragEngineConfig`
|

## Methods

### GetRagEngineConfigRequest

`GetRagEngineConfigRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagEngineConfig

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndexRef -->

# Class DeployedIndexRef (1.135.0)

`DeployedIndexRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Immutable. A resource name of the IndexEndpoint. |
`deployed_index_id` |
`str`
Immutable. The ID of the DeployedIndex in the above IndexEndpoint. |
`display_name` |
`str`
Output only. The display name of the DeployedIndex. |

## Methods

### DeployedIndexRef

`DeployedIndexRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertConfig -->

# Class ModelMonitoringAlertConfig (1.135.0)

`ModelMonitoringAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The alert config for model monitoring.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`email_alert_config` |
Email alert config. This field is a member of `oneof` _ `alert` .
|
`enable_logging` |
`bool`
Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto [
|
`notification_channels` |
`MutableSequence[str]`
Resource names of the NotificationChannels to send alert. Must be of the format `projects/`
|

## Classes

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Methods

### ModelMonitoringAlertConfig

`ModelMonitoringAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The alert config for model monitoring.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsAsyncPager -->

# Class SearchDataItemsAsyncPager (1.135.0)

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchDataItemsAsyncPager

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeatureGroupsPager -->

# Class ListFeatureGroupsPager (1.135.0)

```
ListFeatureGroupsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureGroupsPager

```
ListFeatureGroupsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimesPager -->

# Class ListNotebookRuntimesPager (1.135.0)

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesPager

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingPipeline -->

# Class TrainingPipeline (1.135.0)

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the TrainingPipeline. |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`input_data_config` |
Specifies Vertex AI owned input data that may be used for training the Model. The TrainingPipeline's training_task_definition should make clear whether this config is used and if there are any special requirements on how it should be filled. If nothing about this config is mentioned in the training_task_definition, then it should be assumed that the TrainingPipeline does not depend on this configuration. |
`training_task_definition` |
`str`
Required. A Google Cloud Storage path to the YAML file that defines the training task which is responsible for producing the model artifact, and may also include additional auxiliary work. The definition files that can be used here are found in gs://google-cloud-aiplatform/schema/trainingjob/definition/. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access. |
`training_task_inputs` |
`google.protobuf.struct_pb2.Value`
Required. The training task's parameter(s), as specified in the training_task_definition's `inputs` .
|
`training_task_metadata` |
`google.protobuf.struct_pb2.Value`
Output only. The metadata information as specified in the training_task_definition's `metadata` . This metadata is an auxiliary runtime and
final information about the training task. While the
pipeline is running this information is populated only at a
best effort basis. Only present if the pipeline's
training_task_definition
contains `metadata` object.
|
`model_to_upload` |
Describes the Model that may be uploaded (via ModelService.UploadModel) by this TrainingPipeline. The TrainingPipeline's training_task_definition should make clear whether this Model description should be populated, and if there are any special requirements regarding how it should be filled. If nothing is mentioned in the training_task_definition, then it should be assumed that this field should not be filled and the training task either uploads the Model without a need of this information, or that training task does not support uploading a Model as part of the pipeline. When the Pipeline's state becomes `PIPELINE_STATE_SUCCEEDED` and the trained Model had been
uploaded into Vertex AI, then the model_to_upload's resource
name is populated.
The Model is always uploaded into the Project and Location
in which this pipeline is.
|
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|
`parent_model` |
`str`
Optional. When specify this field, the `model_to_upload`
will not be uploaded as a new model, instead, it will become
a new version of this `parent_model` .
|
`state` |
Output only. The detailed state of the pipeline. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the pipeline's state is `PIPELINE_STATE_FAILED` or `PIPELINE_STATE_CANCELLED` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline for the first time entered the `PIPELINE_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline entered any of the following states: `PIPELINE_STATE_SUCCEEDED` ,
`PIPELINE_STATE_FAILED` , `PIPELINE_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key spec for a TrainingPipeline. If set, this TrainingPipeline will be secured by this key. Note: Model trained by this TrainingPipeline is also secured by this key if model_to_upload is not set separately. |

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

### TrainingPipeline

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsAsyncPager -->

# Class ListDataItemsAsyncPager (1.135.0)

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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


A pager for iterating through `list_data_items`

requests.

This class thinly wraps an initial
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_items`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDataItems`

requests and continue to iterate
through the `data_items`

field on the
corresponding responses.

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataItemsAsyncPager

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionsAsyncPager -->

# Class ListModelVersionsAsyncPager (1.135.0)

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse,
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


A pager for iterating through `list_model_versions`

requests.

This class thinly wraps an initial
[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersions`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionsAsyncPager

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest -->

# Class RetrieveMemoriesRequest (1.135.0)

`RetrieveMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.RetrieveMemories.

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
`similarity_search_params` |
Parameters for semantic similarity search based retrieval. This field is a member of `oneof` _ `retrieval_params` .
|
`simple_retrieval_params` |
Parameters for simple (non-similarity search) retrieval. This field is a member of `oneof` _ `retrieval_params` .
|
`parent` |
`str`
Required. The resource name of the ReasoningEngine to retrieve memories from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`scope` |
`MutableMapping[str, str]`
Required. The scope of the memories to retrieve. A memory must have exactly the same scope ( `Memory.scope` ) as the
scope provided here to be retrieved (same keys and values).
Order does not matter, but it is case-sensitive.
|

## Classes

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

### SimilaritySearchParams

`SimilaritySearchParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for semantic similarity search based retrieval.

### SimpleRetrievalParams

`SimpleRetrievalParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for simple (non-similarity search) retrieval.

## Methods

### RetrieveMemoriesRequest

`RetrieveMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.RetrieveMemories.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardRunsPager -->

# Class ListTensorboardRunsPager (1.135.0)

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

## Methods

### ListTensorboardRunsPager

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesAsyncPager -->

# Class SearchFeaturesAsyncPager (1.135.0)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchFeaturesAsyncPager

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig.SparseEmbeddingConfig.Bm25 -->

# Class Bm25 (1.135.0)

`Bm25(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message for BM25 parameters.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`multilingual` |
`bool`
Optional. Use multilingual tokenizer if set to true. |
`k1` |
`float`
Optional. The parameter to control term frequency saturation. It determines the scaling between the matching term frequency and final score. k1 is in the range of [1.2, 3]. The default value is 1.2. This field is a member of `oneof` _ `_k1` .
|
`b` |
`float`
Optional. The parameter to control document length normalization. It determines how much the document length affects the final score. b is in the range of [0, 1]. The default value is 0.75. This field is a member of `oneof` _ `_b` .
|

## Methods

### Bm25

`Bm25(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message for BM25 parameters.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenAiAdvancedFeaturesConfig.RagConfig -->

# Class RagConfig (1.135.0)

`RagConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Retrieval Augmented Generation feature.

## Attribute |
|
|---|---|
Name |
Description |
`enable_rag` |
`bool`
If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used. |

## Methods

### RagConfig

`RagConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Retrieval Augmented Generation feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePipelineJobRequest -->

# Class DeletePipelineJobRequest (1.135.0)

`DeletePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.DeletePipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### DeletePipelineJobRequest

`DeletePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.DeletePipelineJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrainingPipeline -->

# Class TrainingPipeline (1.135.0)

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the TrainingPipeline. |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`input_data_config` |
Specifies Vertex AI owned input data that may be used for training the Model. The TrainingPipeline's training_task_definition should make clear whether this config is used and if there are any special requirements on how it should be filled. If nothing about this config is mentioned in the training_task_definition, then it should be assumed that the TrainingPipeline does not depend on this configuration. |
`training_task_definition` |
`str`
Required. A Google Cloud Storage path to the YAML file that defines the training task which is responsible for producing the model artifact, and may also include additional auxiliary work. The definition files that can be used here are found in gs://google-cloud-aiplatform/schema/trainingjob/definition/. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access. |
`training_task_inputs` |
`google.protobuf.struct_pb2.Value`
Required. The training task's parameter(s), as specified in the training_task_definition's `inputs` .
|
`training_task_metadata` |
`google.protobuf.struct_pb2.Value`
Output only. The metadata information as specified in the training_task_definition's `metadata` . This metadata is an auxiliary runtime and
final information about the training task. While the
pipeline is running this information is populated only at a
best effort basis. Only present if the pipeline's
training_task_definition
contains `metadata` object.
|
`model_to_upload` |
Describes the Model that may be uploaded (via ModelService.UploadModel) by this TrainingPipeline. The TrainingPipeline's training_task_definition should make clear whether this Model description should be populated, and if there are any special requirements regarding how it should be filled. If nothing is mentioned in the training_task_definition, then it should be assumed that this field should not be filled and the training task either uploads the Model without a need of this information, or that training task does not support uploading a Model as part of the pipeline. When the Pipeline's state becomes `PIPELINE_STATE_SUCCEEDED` and the trained Model had been
uploaded into Vertex AI, then the model_to_upload's resource
name is
populated. The Model is always uploaded into the Project and
Location in which this pipeline is.
|
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|
`parent_model` |
`str`
Optional. When specify this field, the `model_to_upload`
will not be uploaded as a new model, instead, it will become
a new version of this `parent_model` .
|
`state` |
Output only. The detailed state of the pipeline. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the pipeline's state is `PIPELINE_STATE_FAILED` or `PIPELINE_STATE_CANCELLED` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline for the first time entered the `PIPELINE_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline entered any of the following states: `PIPELINE_STATE_SUCCEEDED` ,
`PIPELINE_STATE_FAILED` , `PIPELINE_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TrainingPipeline was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key spec for a TrainingPipeline. If set, this TrainingPipeline will be secured by this key. Note: Model trained by this TrainingPipeline is also secured by this key if model_to_upload is not set separately. |

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

### TrainingPipeline

`TrainingPipeline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The TrainingPipeline orchestrates tasks associated with training a Model. It always executes the training task, and optionally may also export data from Vertex AI's Dataset which becomes the training input, upload the Model to Vertex AI, and evaluate the Model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListArtifactsAsyncPager -->

# Class ListArtifactsAsyncPager (1.135.0)

```
ListArtifactsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
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


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse) object, and
provides an `__aiter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListArtifactsAsyncPager

```
ListArtifactsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesAsyncPager -->

# Class ListSchedulesAsyncPager (1.135.0)

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse) object, and
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

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSchedulesAsyncPager

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager -->

# Class ListEndpointsAsyncPager (1.135.0)

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse) object, and
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

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEndpointsAsyncPager

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsPager -->

# Class ListIndexEndpointsPager (1.135.0)

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexEndpointsPager

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesOperationMetadata -->

# Class ExportFeatureValuesOperationMetadata (1.135.0)

```
ExportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that exports Features values.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore export Feature values. |

## Methods

### ExportFeatureValuesOperationMetadata

```
ExportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that exports Features values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetRequest -->

# Class CreateDatasetRequest (1.135.0)

`CreateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDataset.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Dataset in. Format: `projects/{project}/locations/{location}`
|
`dataset` |
Required. The Dataset to create. |

## Methods

### CreateDatasetRequest

`CreateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse -->

# Class ReadTensorboardUsageResponse (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesAsyncPager -->

# Class ListMemoriesAsyncPager (1.135.0)

```
ListMemoriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


A pager for iterating through `list_memories`

requests.

This class thinly wraps an initial
[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`memories`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMemories`

requests and continue to iterate
through the `memories`

field on the
corresponding responses.

All the usual [ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMemoriesAsyncPager

```
ListMemoriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig.LlmParser -->

# Class LlmParser (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateResponse -->

# Class CheckTrialEarlyStoppingStateResponse (1.135.0)

```
CheckTrialEarlyStoppingStateResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for VizierService.CheckTrialEarlyStoppingState.

## Attribute |
|
|---|---|
Name |
Description |
`should_stop` |
`bool`
True if the Trial should stop. |

## Methods

### CheckTrialEarlyStoppingStateResponse

```
CheckTrialEarlyStoppingStateResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for VizierService.CheckTrialEarlyStoppingState.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.PassThroughField -->

# Class PassThroughField (1.135.0)

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

## Attribute |
|
|---|---|
Name |
Description |
`field_name` |
`str`
Required. The name of the field in the CSV header or the name of the column in BigQuery table. The naming restriction is the same as Feature.name. |

## Methods

### PassThroughField

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataStoresPager -->

# Class ListMetadataStoresPager (1.135.0)

```
ListMetadataStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
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


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataStoresPager

```
ListMetadataStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointOperationMetadata -->

# Class UpdateEndpointOperationMetadata (1.135.0)

```
UpdateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UpdateEndpointLongRunning.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateEndpointOperationMetadata

```
UpdateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UpdateEndpointLongRunning.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRequest -->

# Class DeleteTensorboardRequest (1.135.0)

`DeleteTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Tensorboard to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### DeleteTensorboardRequest

`DeleteTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboard.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationHelpfulnessInput -->

# Class SummarizationHelpfulnessInput (1.135.0)

```
SummarizationHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for summarization helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization helpfulness score metric. |
`instance` |
Required. Summarization helpfulness instance. |

## Methods

### SummarizationHelpfulnessInput

```
SummarizationHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for summarization helpfulness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluation.ModelEvaluationExplanationSpec -->

# Class ModelEvaluationExplanationSpec (1.135.0)

```
ModelEvaluationExplanationSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`explanation_type` |
`str`
Explanation type. For AutoML Image Classification models, possible values are: - `image-integrated-gradients`
- `image-xrai`
|
`explanation_spec` |
Explanation spec details. |

## Methods

### ModelEvaluationExplanationSpec

```
ModelEvaluationExplanationSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager -->

# Class ListTuningJobsAsyncPager (1.135.0)

```
ListTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTuningJobsAsyncPager

```
ListTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint -->

# Class Endpoint (1.135.0)

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Endpoint. |
`display_name` |
`str`
Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Endpoint. |
`deployed_models` |
`MutableSequence[`
Output only. The models deployed in this Endpoint. To add or remove DeployedModels use EndpointService.DeployModel and EndpointService.UndeployModel respectively. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key. |
`network` |
`str`
Optional. The full name of the Google Compute Engine `network ` __
to which the Endpoint should be peered.
Private services access must already be configured for the
network. If left unspecified, the Endpoint is not peered
with any network.
Only one of the fields,
network or
enable_private_service_connect,
can be set.
`Format ` __:
`projects/{project}/global/networks/{network}` . Where
`{project}` is a project number, as in `12345` , and
`{network}` is network name.
|
`enable_private_service_connect` |
`bool`
Deprecated: If true, expose the Endpoint via private service connect. Only one of the fields, network or enable_private_service_connect, can be set. |
`private_service_connect_config` |
Optional. Configuration for private service connect. network and private_service_connect_config are mutually exclusive. |
`model_deployment_monitoring_job` |
`str`
Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by JobService.CreateModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|
`predict_request_response_logging_config` |
Configures the request-response logging for online prediction. |
`dedicated_endpoint_enabled` |
`bool`
If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon. |
`dedicated_endpoint_dns` |
`str`
Output only. DNS of the dedicated endpoint. Will only be populated if dedicated_endpoint_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast_tryout is enabled, uid will be fasttryout. Format: `https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog` .
|
`client_connection_config` |
Configurations that are applied to the endpoint for online prediction. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`gen_ai_advanced_features_config` |
Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported. |
`private_model_server_enabled` |
`bool`
If true, the model server will be isolated from the external internet. |

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

### Endpoint

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMetadataStoreRequest -->

# Class GetMetadataStoreRequest (1.135.0)

`GetMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetMetadataStore.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the MetadataStore to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|

## Methods

### GetMetadataStoreRequest

`GetMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetMetadataStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualitySpec -->

# Class SummarizationQualitySpec (1.135.0)

`SummarizationQualitySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization quality score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute summarization quality. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SummarizationQualitySpec

`SummarizationQualitySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesPayload -->

# Class WriteFeatureValuesPayload (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesAsyncPager -->

# Class ListSavedQueriesAsyncPager (1.135.0)

```
ListSavedQueriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse,
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


A pager for iterating through `list_saved_queries`

requests.

This class thinly wraps an initial
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`saved_queries`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSavedQueries`

requests and continue to iterate
through the `saved_queries`

field on the
corresponding responses.

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSavedQueriesAsyncPager

```
ListSavedQueriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint -->

# Class Endpoint (1.135.0)

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Endpoint. |
`display_name` |
`str`
Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Endpoint. |
`deployed_models` |
`MutableSequence[`
Output only. The models deployed in this Endpoint. To add or remove DeployedModels use EndpointService.DeployModel and EndpointService.UndeployModel respectively. |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Endpoint was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key. |
`network` |
`str`
Optional. The full name of the Google Compute Engine `network ` __
to which the Endpoint should be peered.
Private services access must already be configured for the
network. If left unspecified, the Endpoint is not peered
with any network.
Only one of the fields,
network
or
enable_private_service_connect,
can be set.
`Format ` __:
`projects/{project}/global/networks/{network}` . Where
`{project}` is a project number, as in `12345` , and
`{network}` is network name.
|
`enable_private_service_connect` |
`bool`
Deprecated: If true, expose the Endpoint via private service connect. Only one of the fields, network or enable_private_service_connect, can be set. |
`private_service_connect_config` |
Optional. Configuration for private service connect. network and private_service_connect_config are mutually exclusive. |
`model_deployment_monitoring_job` |
`str`
Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by JobService.CreateModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|
`predict_request_response_logging_config` |
Configures the request-response logging for online prediction. |
`dedicated_endpoint_enabled` |
`bool`
If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon. |
`dedicated_endpoint_dns` |
`str`
Output only. DNS of the dedicated endpoint. Will only be populated if dedicated_endpoint_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast_tryout is enabled, uid will be fasttryout. Format: `https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog` .
|
`client_connection_config` |
Configurations that are applied to the endpoint for online prediction. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`gen_ai_advanced_features_config` |
Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported. |
`private_model_server_enabled` |
`bool`
If true, the model server will be isolated from the external internet. |

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

### Endpoint

`Endpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsPager -->

# Class ListDataLabelingJobsPager (1.135.0)

```
ListDataLabelingJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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


A pager for iterating through `list_data_labeling_jobs`

requests.

This class thinly wraps an initial
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_labeling_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDataLabelingJobs`

requests and continue to iterate
through the `data_labeling_jobs`

field on the
corresponding responses.

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataLabelingJobsPager

```
ListDataLabelingJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataResponse.TuningValidationAssessmentResult -->

# Class TuningValidationAssessmentResult (1.135.0)

```
TuningValidationAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the tuning validation assessment.

## Attribute |
|
|---|---|
Name |
Description |
`errors` |
`MutableSequence[str]`
Optional. A list containing the first validation errors. |

## Methods

### TuningValidationAssessmentResult

```
TuningValidationAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the tuning validation assessment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig.Enterprise -->

# Class Enterprise (1.135.0)

`Enterprise(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Enterprise tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

## Methods

### Enterprise

`Enterprise(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Enterprise tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.DoubleValueSpec -->

# Class DoubleValueSpec (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.JiraSource -->

# Class JiraSource (1.135.0)

`JiraSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Jira source for the ImportRagFilesRequest.

## Attribute |
|
|---|---|
Name |
Description |
`jira_queries` |
`MutableSequence[`
Required. The Jira queries. |

## Classes

### JiraQueries

`JiraQueries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


JiraQueries contains the Jira queries and corresponding authentication.

## Methods

### JiraSource

`JiraSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Jira source for the ImportRagFilesRequest.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec.MetricSpec -->

# Class MetricSpec (1.135.0)

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

## Attributes |
|
|---|---|
Name |
Description |
`metric_id` |
`str`
Required. The ID of the metric. Must not contain whitespaces. |
`goal` |
Required. The optimization goal of the metric. |

## Classes

### GoalType

`GoalType(value)`


The available types of optimization goals.

## Methods

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExtensionRequest -->

# Class DeleteExtensionRequest (1.135.0)

`DeleteExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.DeleteExtension.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Extension resource to be deleted. Format: `projects/{project}/locations/{location}/extensions/{extension}`
|

## Methods

### DeleteExtensionRequest

`DeleteExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.DeleteExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelEvaluationRequest -->

# Class GetModelEvaluationRequest (1.135.0)

`GetModelEvaluationRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModelEvaluation.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelEvaluation resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|

## Methods

### GetModelEvaluationRequest

`GetModelEvaluationRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModelEvaluation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesAsyncPager -->

# Class ListFeaturesAsyncPager (1.135.0)

```
ListFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesAsyncPager

```
ListFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresPager -->

# Class ListFeaturestoresPager (1.135.0)

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse) object, and
provides an `__iter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturestoresPager

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingSupport -->

# Class GroundingSupport (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationVerbosityInstance -->

# Class SummarizationVerbosityInstance (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution -->

# Class Execution (1.135.0)

```
Execution(
execution_name: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
)
```


Metadata Execution resource for Vertex AI

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

### state

State of this Execution.

### update_time

Time this resource was last updated.

## Methods

### Execution

```
Execution(
execution_name: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
)
```


Retrieves an existing Metadata Execution given a resource name or ID.

Parameters |
|
|---|---|
Name |
Description |
`execution_name` |
`str`
Required. A fully-qualified resource name or resource ID of the Execution. Example: "projects/123/locations/us-central1/metadataStores/default/executions/my-resource". or "my-resource" when project and location are initialized or passed. |
`metadata_store_id` |
`str`
Optional. MetadataStore to retrieve Execution from. If not set, metadata_store_id is set to "default". If execution_name is a fully-qualified resource, its metadata_store_id overrides this one. |
`project` |
`str`
Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve the Execution from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Execution. Overrides credentials set in aiplatform.init. |

### assign_input_artifacts

```
assign_input_artifacts(
artifacts: typing.List[
typing.Union[
google.cloud.aiplatform.metadata.artifact.Artifact,
google.cloud.aiplatform.models.Model,
]
],
)
```


Assigns Artifacts as inputs to this Executions.

Parameter |
|
|---|---|
Name |
Description |
`artifacts` |
`List[Union[artifact.Artifact, models.Model]]`
Required. Artifacts to assign as input. |

### assign_output_artifacts

```
assign_output_artifacts(
artifacts: typing.List[
typing.Union[
google.cloud.aiplatform.metadata.artifact.Artifact,
google.cloud.aiplatform.models.Model,
]
],
)
```


Assigns Artifacts as outputs to this Executions.

Parameter |
|
|---|---|
Name |
Description |
`artifacts` |
`List[Union[artifact.Artifact, models.Model]]`
Required. Artifacts to assign as input. |

### create

```
create(
schema_title: str,
*,
state: google.cloud.aiplatform_v1.types.execution.Execution.State = State.RUNNING,
resource_id: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict[str, typing.Any]] = None,
description: typing.Optional[str] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials=typing.Optional[google.auth.credentials.Credentials]
) -> google.cloud.aiplatform.metadata.execution.Execution
```


Creates a new Metadata Execution.

Parameters |
|
|---|---|
Name |
Description |
`schema_title` |
`str`
Required. schema_title identifies the schema title used by the Execution. |
`state` |
`gca_execution.Execution.State.RUNNING`
Optional. State of this Execution. Defaults to RUNNING. |
`resource_id` |
`str`
Optional. The <resource_id> portion of the Execution name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/executions/<resource_id>. |
`display_name` |
`str`
Optional. The user-defined name of the Execution. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the Execution. If not set, defaults to use the latest version. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the Execution. |
`description` |
`str`
Optional. Describes the purpose of the Execution to be created. |
`metadata_store_id` |
`str`
Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Optional. Project used to create this Execution. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location used to create this Execution. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials used to create this Execution. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`Execution` |
Instantiated representation of the managed Metadata Execution. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### get

```
get(
resource_id: str,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.metadata.resource._Resource
```


Retrieves a Metadata resource.

Parameters |
|
|---|---|
Name |
Description |
`resource_id` |
`str`
Required. The <resource_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id>. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to retrieve or create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to retrieve or create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to retrieve or create this resource. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`resource (_Resource)` |
Instantiated representation of the managed Metadata resource or None if no resource was found. |

### get_input_artifacts

```
get_input_artifacts() -> (
typing.List[google.cloud.aiplatform.metadata.artifact.Artifact]
)
```


Get the input Artifacts of this Execution.

### get_or_create

```
get_or_create(
resource_id: str,
schema_title: str,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.metadata.resource._Resource
```


Retrieves or Creates (if it does not exist) a Metadata resource.

Parameters |
|
|---|---|
Name |
Description |
`resource_id` |
`str`
Required. The <resource_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id>. |
`schema_title` |
`str`
Required. schema_title identifies the schema title used by the resource. |
`display_name` |
`str`
Optional. The user-defined name of the resource. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the resource. If not set, defaults to use the latest version. |
`description` |
`str`
Optional. Describes the purpose of the resource to be created. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the resource. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to retrieve or create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to retrieve or create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to retrieve or create this resource. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`resource (_Resource)` |
Instantiated representation of the managed Metadata resource. |

### get_output_artifacts

```
get_output_artifacts() -> (
typing.List[google.cloud.aiplatform.metadata.artifact.Artifact]
)
```


Get the output Artifacts of this Execution.

### list

```
list(
filter: typing.Optional[str] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
order_by: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.metadata.resource._Resource]
```


List resources that match the list filter in target metadataStore.

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. A query to filter available resources for matching results. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to create this resource. Overrides credentials set in aiplatform.init. |
`order_by` |
`str`
Optional. How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a |

Returns |
|
|---|---|
Type |
Description |
`resources (sequence[_Resource])` |
a list of managed Metadata resource. |

### sync_resource

`sync_resource()`


Syncs local resource with the resource in metadata store.

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
state: typing.Optional[
google.cloud.aiplatform_v1.types.execution.Execution.State
] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict[str, typing.Any]] = None,
)
```


Update this Execution.

Parameters |
|
|---|---|
Name |
Description |
`state` |
`gca_execution.Execution.State`
Optional. State of this Execution. |
`description` |
`str`
Optional. Describes the purpose of the Execution to be created. |
`metadata` |
`Dict[str, Any`
Optional. Contains the metadata information that will be stored in the Execution. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob -->

# Class TimeSeriesDenseEncoderForecastingTrainingJob (1.135.0)

```
TimeSeriesDenseEncoderForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Time series Dense Encoder (TiDE) forecasting models.

The `TimeSeriesDenseEncoderForecastingTrainingJob`

class uses the
Time-series Dense Encoder (TiDE) training method to train and run a
forecasting model. TiDE uses a
[multi-layer perceptron](https://arxiv.org/abs/2304.08424) (MLP) to provide
the speed of forecasting linear models with covariates and non-linear
dependencies. For more information about TiDE, see
[Recent advances in deep long-horizon forecasting](https://blog.research.google/2023/04/recent-advances-in-deep-long-horizon.html)
and this
[TiDE blog post](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-forecasting).

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### TimeSeriesDenseEncoderForecastingTrainingJob

```
TimeSeriesDenseEncoderForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesAsyncPager -->

# Class ListFeaturesAsyncPager (1.135.0)

```
ListFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesAsyncPager

```
ListFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse -->

# Class ReadTensorboardUsageResponse (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs.ModelType -->

# Class ModelType (1.135.0)

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

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-28 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager -->

# Class ListPipelineJobsAsyncPager (1.135.0)

```
ListPipelineJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse) object, and
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

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPipelineJobsAsyncPager

```
ListPipelineJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.FeatureRegistrySource -->

# Class FeatureRegistrySource (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndexRef -->

# Class DeployedIndexRef (1.135.0)

`DeployedIndexRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Immutable. A resource name of the IndexEndpoint. |
`deployed_index_id` |
`str`
Immutable. The ID of the DeployedIndex in the above IndexEndpoint. |
`display_name` |
`str`
Output only. The display name of the DeployedIndex. |

## Methods

### DeployedIndexRef

`DeployedIndexRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteSavedQueryRequest -->

# Class DeleteSavedQueryRequest (1.135.0)

`DeleteSavedQueryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteSavedQuery.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SavedQuery to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/savedQueries/{saved_query}`
|

## Methods

### DeleteSavedQueryRequest

`DeleteSavedQueryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteSavedQuery.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput -->

# Class ModelMonitoringInput (1.135.0)

`ModelMonitoringInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model monitoring data input spec.

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
`columnized_dataset` |
Columnized dataset. This field is a member of `oneof` _ `dataset` .
|
`batch_prediction_output` |
Vertex AI Batch prediction Job. This field is a member of `oneof` _ `dataset` .
|
`vertex_endpoint_logs` |
Vertex AI Endpoint request & response logging. This field is a member of `oneof` _ `dataset` .
|
`time_interval` |
`google.type.interval_pb2.Interval`
The time interval (pair of start_time and end_time) for which results should be returned. This field is a member of `oneof` _ `time_spec` .
|
`time_offset` |
The time offset setting for which results should be returned. This field is a member of `oneof` _ `time_spec` .
|

## Classes

### BatchPredictionOutput

`BatchPredictionOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Batch prediction job output.

### ModelMonitoringDataset

`ModelMonitoringDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input dataset spec.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TimeOffset

`TimeOffset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time offset setting.

### VertexEndpointLogs

`VertexEndpointLogs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Endpoint request response logging.

## Methods

### ModelMonitoringInput

`ModelMonitoringInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model monitoring data input spec.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.IntegerValueSpec -->

# Class IntegerValueSpec (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse -->

# Class ListIndexesResponse (1.135.0)

`ListIndexesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexService.ListIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`indexes` |
`MutableSequence[`
List of indexes in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListIndexesRequest.page_token to obtain that page. |

## Methods

### ListIndexesResponse

`ListIndexesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexService.ListIndexes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenAiAdvancedFeaturesConfig.RagConfig -->

# Class RagConfig (1.135.0)

`RagConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Retrieval Augmented Generation feature.

## Attribute |
|
|---|---|
Name |
Description |
`enable_rag` |
`bool`
If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used. |

## Methods

### RagConfig

`RagConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Retrieval Augmented Generation feature.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager -->

# Class ListTrainingPipelinesPager (1.135.0)

```
ListTrainingPipelinesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
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
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse) object, and
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

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrainingPipelinesPager

```
ListTrainingPipelinesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsPager -->

# Class ListDatasetVersionsPager (1.135.0)

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse) object, and
provides an `__iter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDatasetVersions`

requests and continue to iterate
through the `dataset_versions`

field on the
corresponding responses.

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetVersionsPager

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient -->

# Class IndexEndpointServiceClient (1.135.0)

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's IndexEndpoints.

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
`IndexEndpointServiceTransport` |
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

### IndexEndpointServiceClient

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index endpoint service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexEndpointServiceTransport,Callable[..., IndexEndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexEndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index_endpoint

```
create_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.CreateIndexEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
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


Creates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1.[CreateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexEndpointRequest.html)(
parent="parent_value",
index_endpoint=index_endpoint,
)
# Make the request
operation = client.[create_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_create_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.CreateIndexEndpoint. |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: |
`index_endpoint` |
Required. The IndexEndpoint to create. This corresponds to the |
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

### delete_index_endpoint

```
delete_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.DeleteIndexEndpointRequest,
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


Deletes an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_delete_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.DeleteIndexEndpoint. |
`name` |
`str`
Required. The name of the IndexEndpoint resource to be deleted. Format: |
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

### deploy_index

```
deploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.DeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.DeployedIndex
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


Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it. Only non-empty Indexes can be deployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_deploy_index():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1.[DeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[deploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_deploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.DeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be created within the IndexEndpoint. This corresponds to the |
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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

### get_index_endpoint

```
get_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.GetIndexEndpointRequest,
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
) -> google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
```


Gets an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_get_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.GetIndexEndpoint |
`name` |
`str`
Required. The name of the IndexEndpoint resource. Format: |
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
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_index_endpoints

```
list_index_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
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
google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsPager
)
```


Lists IndexEndpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_index_endpoints():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListIndexEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_index_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_list_index_endpoints)(request=request)
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
The request object. Request message for IndexEndpointService.ListIndexEndpoints. |
`parent` |
`str`
Required. The resource name of the Location from which to list the IndexEndpoints. Format: |
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
Response message for IndexEndpointService.ListIndexEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### mutate_deployed_index

```
mutate_deployed_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.MutateDeployedIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.DeployedIndex
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


Update an existing DeployedIndex under an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_mutate_deployed_index():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1.[MutateDeployedIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[mutate_deployed_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_mutate_deployed_index)(request=request)
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
The request object. Request message for IndexEndpointService.MutateDeployedIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are DeployedIndex.automatic_resources and DeployedIndex.dedicated_resources This corresponds to the |
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

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### parse_index_path

`parse_index_path(path: str) -> typing.Dict[str, str]`


Parses a index path into its component segments.

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

### undeploy_index

```
undeploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.UndeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index_id: typing.Optional[str] = None,
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


Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_undeploy_index():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UndeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index_id="deployed_index_id_value",
)
# Make the request
operation = client.[undeploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_undeploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.UndeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. This corresponds to the |
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

### update_index_endpoint

```
update_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_endpoint_service.UpdateIndexEndpointRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
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
) -> google.cloud.aiplatform_v1.types.index_endpoint.IndexEndpoint
```


Updates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_index_endpoint():
# Create a client
client = aiplatform_v1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexEndpointRequest.html)(
index_endpoint=index_endpoint,
)
# Make the request
response = client.[update_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1_services_index_endpoint_service_IndexEndpointServiceClient_update_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.UpdateIndexEndpoint. |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See |
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
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNasTrialDetailRequest -->

# Class GetNasTrialDetailRequest (1.135.0)

`GetNasTrialDetailRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasTrialDetail.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasTrialDetail resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}/nasTrialDetails/{nas_trial_detail}`
|

## Methods

### GetNasTrialDetailRequest

`GetNasTrialDetailRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasTrialDetail.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionInput -->

# Class TrajectoryPrecisionInput (1.135.0)

`TrajectoryPrecisionInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryPrecision metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for TrajectoryPrecision metric. |
`instances` |
`MutableSequence[`
Required. Repeated TrajectoryPrecision instance. |

## Methods

### TrajectoryPrecisionInput

`TrajectoryPrecisionInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryPrecision metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesOperationMetadata -->

# Class BatchMigrateResourcesOperationMetadata (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListExecutionsAsyncPager -->

# Class ListExecutionsAsyncPager (1.135.0)

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsAsyncPager

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresPager -->

# Class ListExampleStoresPager (1.135.0)

```
ListExampleStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
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


A pager for iterating through `list_example_stores`

requests.

This class thinly wraps an initial
[ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`example_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExampleStores`

requests and continue to iterate
through the `example_stores`

field on the
corresponding responses.

All the usual [ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExampleStoresPager

```
ListExampleStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationsPager -->

# Class ListModelEvaluationsPager (1.135.0)

```
ListModelEvaluationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
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


A pager for iterating through `list_model_evaluations`

requests.

This class thinly wraps an initial
[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_evaluations`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelEvaluations`

requests and continue to iterate
through the `model_evaluations`

field on the
corresponding responses.

All the usual [ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationsPager

```
ListModelEvaluationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrivateServiceConnectConfig -->

# Class PrivateServiceConnectConfig (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.DoubleValueSpec -->

# Class DoubleValueSpec (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesPayload -->

# Class WriteFeatureValuesPayload (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityInstance -->

# Class SummarizationVerbosityInstance (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetRequest -->

# Class CreateDatasetRequest (1.135.0)

`CreateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDataset.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Dataset in. Format: `projects/{project}/locations/{location}`
|
`dataset` |
Required. The Dataset to create. |

## Methods

### CreateDatasetRequest

`CreateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringQualityInput -->

# Class QuestionAnsweringQualityInput (1.135.0)

```
QuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering quality score metric. |
`instance` |
Required. Question answering quality instance. |

## Methods

### QuestionAnsweringQualityInput

```
QuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering quality metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingSupport -->

# Class GroundingSupport (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsPager -->

# Class ListBatchPredictionJobsPager (1.135.0)

```
ListBatchPredictionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
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


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListBatchPredictionJobsPager

```
ListBatchPredictionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob -->

# Class TemporalFusionTransformerForecastingTrainingJob (1.135.0)

```
TemporalFusionTransformerForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Temporal Fusion Transformer (TFT) forecasting models.

The `TemporalFusionTransformerForecastingTrainingJob`

class uses the
Temporal Fusion Transformer (TFT) training method to train and run a
forecasting model. The TFT training method implements an attention-based
deep neural network (DNN) model that uses a multi-horizon forecasting task
to produce predictions.

For sample code that shows you how to use
`TemporalFusionTransformerForecastingTrainingJob, see the
[Create a training pipeline forecasting temporal fusion transformer
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_tft_sample.py)
on GitHub.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### TemporalFusionTransformerForecastingTrainingJob

```
TemporalFusionTransformerForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataSchemasPager -->

# Class ListMetadataSchemasPager (1.135.0)

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataSchemasPager

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest -->

# Class DeletePipelineJobRequest (1.135.0)

`DeletePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.DeletePipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### DeletePipelineJobRequest

`DeletePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.DeletePipelineJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessInput -->

# Class SummarizationHelpfulnessInput (1.135.0)

```
SummarizationHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for summarization helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization helpfulness score metric. |
`instance` |
Required. Summarization helpfulness instance. |

## Methods

### SummarizationHelpfulnessInput

```
SummarizationHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for summarization helpfulness metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.VertexFeatureStore -->

# Class VertexFeatureStore (1.135.0)

`VertexFeatureStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Feature Store.

## Attribute |
|
|---|---|
Name |
Description |
`feature_view_resource_name` |
`str`
The resource name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### VertexFeatureStore

`VertexFeatureStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Feature Store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardRunsResponse -->

# Class BatchCreateTensorboardRunsResponse (1.135.0)

```
BatchCreateTensorboardRunsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardRuns.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard_runs` |
`MutableSequence[`
The created TensorboardRuns. |

## Methods

### BatchCreateTensorboardRunsResponse

```
BatchCreateTensorboardRunsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardRuns.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesAsyncPager -->

# Class ListEntityTypesAsyncPager (1.135.0)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesAsyncPager

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager -->

# Class ListRagCorporaAsyncPager (1.135.0)

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagCorporaAsyncPager

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager -->

# Class ListSpecialistPoolsPager (1.135.0)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsPager

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.FeatureRegistrySource -->

# Class FeatureRegistrySource (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.IntegerValueSpec -->

# Class IntegerValueSpec (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.PassThroughField -->

# Class PassThroughField (1.135.0)

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

## Attribute |
|
|---|---|
Name |
Description |
`field_name` |
`str`
Required. The name of the field in the CSV header or the name of the column in BigQuery table. The naming restriction is the same as Feature.name. |

## Methods

### PassThroughField

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse -->

# Class ListAnnotationsResponse (1.135.0)

`ListAnnotationsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListAnnotations.

## Attributes |
|
|---|---|
Name |
Description |
`annotations` |
`MutableSequence[`
A list of Annotations that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListAnnotationsResponse

`ListAnnotationsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListAnnotations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesOperationMetadata -->

# Class BatchMigrateResourcesOperationMetadata (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest -->

# Class ListEventsRequest (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineFailurePolicy -->

# Class PipelineFailurePolicy (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob -->

# Class SequenceToSequencePlusForecastingTrainingJob (1.135.0)

```
SequenceToSequencePlusForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Sequence to Sequence (Seq2Seq) forecasting models.

The `SequenceToSequencePlusForecastingTrainingJob`

class uses the `Seq2seq+`

training method to train and run a forecasting model. The `Seq2seq+`

training method is a good choice for experimentation. Its algorithm is
simpler and uses a smaller search space than the `AutoML`

option. `Seq2seq+`

is a good option if you want fast results and your datasets are smaller than
1 GB.

For sample code that shows you how to use
`SequenceToSequencePlusForecastingTrainingJob`

, see the [Create a training
pipeline forecasting Seq2seq
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_seq2seq_sample.py)
on GitHub.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### SequenceToSequencePlusForecastingTrainingJob

```
SequenceToSequencePlusForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataSchemasPager -->

# Class ListMetadataSchemasPager (1.134.0)

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataSchemasPager

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePipelineJobRequest -->

# Class DeletePipelineJobRequest (1.134.0)

`DeletePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.DeletePipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob resource to be deleted. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### DeletePipelineJobRequest

`DeletePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.DeletePipelineJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessInput -->

# Class SummarizationHelpfulnessInput (1.134.0)

```
SummarizationHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for summarization helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization helpfulness score metric. |
`instance` |
Required. Summarization helpfulness instance. |

## Methods

### SummarizationHelpfulnessInput

```
SummarizationHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for summarization helpfulness metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.VertexFeatureStore -->

# Class VertexFeatureStore (1.134.0)

`VertexFeatureStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Feature Store.

## Attribute |
|
|---|---|
Name |
Description |
`feature_view_resource_name` |
`str`
The resource name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### VertexFeatureStore

`VertexFeatureStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Feature Store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardRunsResponse -->

# Class BatchCreateTensorboardRunsResponse (1.134.0)

```
BatchCreateTensorboardRunsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardRuns.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard_runs` |
`MutableSequence[`
The created TensorboardRuns. |

## Methods

### BatchCreateTensorboardRunsResponse

```
BatchCreateTensorboardRunsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardRuns.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesAsyncPager -->

# Class ListEntityTypesAsyncPager (1.134.0)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesAsyncPager

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager -->

# Class ListRagCorporaAsyncPager (1.134.0)

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagCorporaAsyncPager

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager -->

# Class ListSpecialistPoolsPager (1.134.0)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsPager

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.FeatureRegistrySource -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.IntegerValueSpec -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.PassThroughField -->

# Class PassThroughField (1.134.0)

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

## Attribute |
|
|---|---|
Name |
Description |
`field_name` |
`str`
Required. The name of the field in the CSV header or the name of the column in BigQuery table. The naming restriction is the same as Feature.name. |

## Methods

### PassThroughField

`PassThroughField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describe pass-through fields in read_instance source.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse -->

# Class ListAnnotationsResponse (1.134.0)

`ListAnnotationsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListAnnotations.

## Attributes |
|
|---|---|
Name |
Description |
`annotations` |
`MutableSequence[`
A list of Annotations that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListAnnotationsResponse

`ListAnnotationsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListAnnotations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesOperationMetadata -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineFailurePolicy -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob -->

# Class SequenceToSequencePlusForecastingTrainingJob (1.134.0)

```
SequenceToSequencePlusForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Class to train Sequence to Sequence (Seq2Seq) forecasting models.

The `SequenceToSequencePlusForecastingTrainingJob`

class uses the `Seq2seq+`

training method to train and run a forecasting model. The `Seq2seq+`

training method is a good choice for experimentation. Its algorithm is
simpler and uses a smaller search space than the `AutoML`

option. `Seq2seq+`

is a good option if you want fast results and your datasets are smaller than
1 GB.

For sample code that shows you how to use
`SequenceToSequencePlusForecastingTrainingJob`

, see the [Create a training
pipeline forecasting Seq2seq
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_seq2seq_sample.py)
on GitHub.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### evaluated_data_items_bigquery_uri

BigQuery location of exported evaluated examples from the Training Job

Returns |
|
|---|---|
Type |
Description |
`str` |
BigQuery uri for the exported evaluated examples if the export feature is enabled for training. None: If the export feature was not enabled for training. |

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### SequenceToSequencePlusForecastingTrainingJob

```
SequenceToSequencePlusForecastingTrainingJob(
display_name: typing.Optional[str] = None,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a Forecasting Training Job.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this TrainingPipeline. |
`optimization_objective` |
`str`
Optional. Objective function the model is to be optimized towards. The training process creates a Model that optimizes the value of the objective function over the validation set. The supported optimization objectives: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). "minimize-rmspe" - Minimize root-mean-squared percentage error (RMSPE). "minimize-wape-mae" - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE). "minimize-quantile-loss" - Minimize the quantile loss at the defined quantiles. (Set this objective to build quantile forecasts.) |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both column_transformations and column_specs were provided. |

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset,
target_column: str,
time_column: str,
time_series_identifier_column: str,
unavailable_at_forecast_columns: typing.List[str],
available_at_forecast_columns: typing.List[str],
forecast_horizon: int,
data_granularity_unit: str,
data_granularity_count: int,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
time_series_attribute_columns: typing.Optional[typing.List[str]] = None,
context_window: typing.Optional[int] = None,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
quantiles: typing.Optional[typing.List[float]] = None,
validation_options: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
additional_experiments: typing.Optional[typing.List[str]] = None,
hierarchy_group_columns: typing.Optional[typing.List[str]] = None,
hierarchy_group_total_weight: typing.Optional[float] = None,
hierarchy_temporal_total_weight: typing.Optional[float] = None,
hierarchy_group_temporal_total_weight: typing.Optional[float] = None,
window_column: typing.Optional[str] = None,
window_stride_length: typing.Optional[int] = None,
window_max_count: typing.Optional[int] = None,
holiday_regions: typing.Optional[typing.List[str]] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
enable_probabilistic_inference: bool = False,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TimeSeriesDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For time series Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. Name of the column that the Model is to predict values for. This column must be unavailable at forecast. |
`time_column` |
`str`
Required. Name of the column that identifies time order in the time series. This column must be available at forecast. |
`time_series_identifier_column` |
`str`
Required. Name of the column that identifies the time series. |
`unavailable_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are unavailable at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is unknown before the forecast (e.g. population of a city in a given year, or weather on a given day). |
`available_at_forecast_columns` |
`List[str]`
Required. Column names of columns that are available at forecast. Each column contains information for the given entity (identified by the [time_series_identifier_column]) that is known at forecast. |
`data_granularity_unit` |
`str`
Required. The data granularity unit. Accepted values are |
`data_granularity_count` |
`int`
Required. The number of data granularity units between data points in the training data. If [data_granularity_unit] is |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`time_series_attribute_columns` |
`List[str]`
Optional. Column names that should be used as attribute columns. Each column is constant within a time series. |
`context_window` |
`int`
Optional. The amount of time into the past training and prediction data is used for model training and prediction respectively. Expressed in number of units defined by the [data_granularity_unit] and [data_granularity_count] fields. When not provided uses the default value of 0 which means the model sets each series context window to be 0 (also known as "cold start"). Inclusive. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`quantiles` |
`List[float]`
Quantiles to use for the |
`validation_options` |
`str`
Validation options for the data validation component. The available options are: "fail-pipeline" - (default), will validate against the validation and fail the pipeline if it fails. "ignore-validation" - ignore the results of the validation and continue the pipeline |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the time series forcasting training. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`hierarchy_group_columns` |
`List[str]`
Optional. A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. |
`hierarchy_group_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over time series in the same hierarchy group. |
`hierarchy_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over the horizon for a single time series. |
`hierarchy_group_temporal_total_weight` |
`float`
Optional. The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group. |
`window_column` |
`str`
Optional. Name of the column that should be used to filter input rows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window from that row. |
`window_stride_length` |
`int`
Optional. Step length used to generate input examples. Every |
`window_max_count` |
`int`
Optional. Number of rows that should be used to generate input examples. If the total row count is larger than this number, the input data will be randomly sampled to hit the count. |
`holiday_regions` |
`List[str]`
Optional. The geographical regions to use when creating holiday features. This option is only allowed when data_granularity_unit is |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_probabilistic_inference` |
`bool`
If probabilistic inference is enabled, the model will fit a distribution that captures the uncertainty of a prediction. At inference time, the predictive distribution is used to make a point prediction that minimizes the optimization objective. For example, the mean of a predictive distribution is the point prediction that minimizes RMSE loss. If quantiles are specified, then the quantiles of the distribution are also returned. The optimization objective cannot be minimize-quantile-loss. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob -->

# Class NotebookExecutionJob (1.134.0)

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

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
`dataform_repository_source` |
The Dataform Repository pointing to a single file notebook repository. This field is a member of `oneof` _ `notebook_source` .
|
`gcs_notebook_source` |
The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
This field is a member of `oneof` _ `notebook_source` .
|
`direct_notebook_source` |
The contents of an input notebook file. This field is a member of `oneof` _ `notebook_source` .
|
`notebook_runtime_template_resource_name` |
`str`
The NotebookRuntimeTemplate to source compute configuration from. This field is a member of `oneof` _ `environment_spec` .
|
`custom_environment_spec` |
The custom compute configuration for an execution job. This field is a member of `oneof` _ `environment_spec` .
|
`gcs_output_uri` |
`str`
The Cloud Storage location to upload the result to. Format: `gs://bucket-name`
This field is a member of `oneof` _ `execution_sink` .
|
`execution_user` |
`str`
The user email to run the execution as. Only supported by Colab runtimes. This field is a member of `oneof` _ `execution_identity` .
|
`service_account` |
`str`
The service account to run the execution as. This field is a member of `oneof` _ `execution_identity` .
|
`workbench_runtime` |
The Workbench runtime configuration to use for the notebook execution. This field is a member of `oneof` _ `runtime_environment` .
|
`name` |
`str`
Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`
|
`display_name` |
`str`
The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`execution_timeout` |
`google.protobuf.duration_pb2.Duration`
Max running time of the execution job in seconds (default 86400s / 24 hrs). |
`schedule_resource_name` |
`str`
The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`
|
`job_state` |
Output only. The state of the NotebookExecutionJob. |
`status` |
`google.rpc.status_pb2.Status`
Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`kernel_name` |
`str`
The name of the kernel to use during notebook execution. If unset, the default kernel is used. |
`encryption_spec` |
Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the NotebookRuntimeTemplate has an encryption spec. |

## Classes

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

### DirectNotebookSource

`DirectNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The content of the input notebook in ipynb format.

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

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

### WorkbenchRuntime

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.

## Methods

### NotebookExecutionJob

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob -->

# Class NotebookExecutionJob (1.134.0)

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

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
`dataform_repository_source` |
The Dataform Repository pointing to a single file notebook repository. This field is a member of `oneof` _ `notebook_source` .
|
`gcs_notebook_source` |
The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
This field is a member of `oneof` _ `notebook_source` .
|
`direct_notebook_source` |
The contents of an input notebook file. This field is a member of `oneof` _ `notebook_source` .
|
`notebook_runtime_template_resource_name` |
`str`
The NotebookRuntimeTemplate to source compute configuration from. This field is a member of `oneof` _ `environment_spec` .
|
`custom_environment_spec` |
The custom compute configuration for an execution job. This field is a member of `oneof` _ `environment_spec` .
|
`gcs_output_uri` |
`str`
The Cloud Storage location to upload the result to. Format: `gs://bucket-name`
This field is a member of `oneof` _ `execution_sink` .
|
`execution_user` |
`str`
The user email to run the execution as. Only supported by Colab runtimes. This field is a member of `oneof` _ `execution_identity` .
|
`service_account` |
`str`
The service account to run the execution as. This field is a member of `oneof` _ `execution_identity` .
|
`workbench_runtime` |
The Workbench runtime configuration to use for the notebook execution. This field is a member of `oneof` _ `runtime_environment` .
|
`name` |
`str`
Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`
|
`display_name` |
`str`
The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`execution_timeout` |
`google.protobuf.duration_pb2.Duration`
Max running time of the execution job in seconds (default 86400s / 24 hrs). |
`schedule_resource_name` |
`str`
The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`
|
`job_state` |
Output only. The state of the NotebookExecutionJob. |
`status` |
`google.rpc.status_pb2.Status`
Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookExecutionJob was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`kernel_name` |
`str`
The name of the kernel to use during notebook execution. If unset, the default kernel is used. |
`encryption_spec` |
Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the NotebookRuntimeTemplate has an encryption spec. |

## Classes

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

### DirectNotebookSource

`DirectNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The content of the input notebook in ipynb format.

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

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

### WorkbenchRuntime

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.

## Methods

### NotebookExecutionJob

`NotebookExecutionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


NotebookExecutionJob represents an instance of a notebook execution.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Execution -->

# Class Execution (1.134.0)

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Execution. |
`display_name` |
`str`
User provided display name of the Execution. May be up to 128 Unicode characters. |
`state` |
The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines) and the system does not prescribe or check the validity of state transitions. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Executions. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was last updated. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in `schema_title` to use.
Schema title and version is expected to be registered in
earlier Create Schema calls. And both are used together as
unique identifiers to identify schemas within the local
metadata store.
|
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Execution |

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


Describes the state of the Execution.

## Methods

### Execution

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsPager -->

# Class ListCachedContentsPager (1.134.0)

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse) object, and
provides an `__iter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCachedContentsPager

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsAsyncPager -->

# Class ListAnnotationsAsyncPager (1.134.0)

```
ListAnnotationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
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


A pager for iterating through `list_annotations`

requests.

This class thinly wraps an initial
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse) object, and
provides an `__aiter__`

method to iterate through its
`annotations`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListAnnotations`

requests and continue to iterate
through the `annotations`

field on the
corresponding responses.

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListAnnotationsAsyncPager

```
ListAnnotationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexAISearch.DataStoreSpec -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SlackSource -->

# Class SlackSource (1.134.0)

`SlackSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Slack source for the ImportRagFilesRequest.

## Attribute |
|
|---|---|
Name |
Description |
`channels` |
`MutableSequence[`
Required. The Slack channels. |

## Classes

### SlackChannels

`SlackChannels(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannels contains the Slack channels and corresponding access token.

## Methods

### SlackSource

`SlackSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Slack source for the ImportRagFilesRequest.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GoogleDriveSource.ResourceId -->

# Class ResourceId (1.134.0)

`ResourceId(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type and ID of the Google Drive resource.

## Attributes |
|
|---|---|
Name |
Description |
`resource_type` |
Required. The type of the Google Drive resource. |
`resource_id` |
`str`
Required. The ID of the Google Drive resource. |

## Classes

### ResourceType

`ResourceType(value)`


The type of the Google Drive resource.

## Methods

### ResourceId

`ResourceId(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type and ID of the Google Drive resource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/prediction_v1 -->

# Types for Google Cloud Aiplatform V1 Schema Predict Prediction v1 API

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Image and Text Classification.

#### ids()

The resource IDs of the AnnotationSpecs that had been identified.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### display_names()

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### confidences()

The Model’s confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### confidences(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### display_names(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### ids(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ImageObjectDetectionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Image Object Detection.

#### ids()

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### display_names()

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### confidences()

The Model’s confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### bboxes()

Bounding boxes, i.e. the rectangles over the image, that
pinpoint the found AnnotationSpecs. Given in order that
matches the IDs. Each bounding box is an array of 4 numbers
`xMin`

, `xMax`

, `yMin`

, and `yMax`

, which represent
the extremal coordinates of the box. They are relative to
the image size, and the point 0,0 is in the top left of the
image.

**Type**MutableSequence[

[google.protobuf.struct_pb2.ListValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/struct_pb2.html#google.protobuf.struct_pb2.ListValue)]

#### bboxes(*: MutableSequence[*[google.protobuf.struct_pb2.ListValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/struct_pb2.html#google.protobuf.struct_pb2.ListValue) )

[google.protobuf.struct_pb2.ListValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/struct_pb2.html#google.protobuf.struct_pb2.ListValue)

#### confidences(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### display_names(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### ids(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ImageSegmentationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Image Segmentation.

#### category_mask()

A PNG image where each pixel in the mask represents the category in which the pixel in the original image was predicted to belong to. The size of this image will be the same as the original image. The mapping between the AnntoationSpec and the color can be found in model’s metadata. The model will choose the most likely category and if none of the categories reach the confidence threshold, the pixel will be marked as background.

**Type**

#### confidence_mask()

A one channel image which is encoded as an 8bit lossless PNG. The size of the image will be the same as the original image. For a specific pixel, darker color means less confidence in correctness of the cateogry in the categoryMask for the corresponding pixel. Black means no confidence and white means complete confidence.

**Type**

#### category_mask(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### confidence_mask(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Tabular Classification.

#### classes()

The name of the classes being classified, contains all possible values of the target column.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### scores()

The model’s confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### classes(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### scores(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularRegressionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Tabular Regression.

#### value()

The regression value.

**Type**

#### lower_bound()

The lower bound of the prediction interval.

**Type**

#### upper_bound()

The upper bound of the prediction interval.

**Type**

#### lower_bound(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### upper_bound(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextExtractionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Text Extraction.

#### ids()

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### display_names()

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### text_segment_start_offsets()

The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### text_segment_end_offsets()

The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### confidences()

The Model’s confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### confidences(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### display_names(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### ids(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

#### text_segment_end_offsets(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

#### text_segment_start_offsets(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextSentimentPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Text Sentiment

#### sentiment()

The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive).

**Type**

#### sentiment(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoActionRecognitionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Video Action Recognition.

#### id()

The resource ID of the AnnotationSpec that had been identified.

**Type**

#### display_name()

The display name of the AnnotationSpec that had been identified.

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### time_segment_end()

The end, exclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### confidence()

The Model’s confidence in correction of this prediction, higher value means higher confidence.

#### confidence(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### display_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### time_segment_start(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Video Classification.

#### id()

The resource ID of the AnnotationSpec that had been identified.

**Type**

#### display_name()

The display name of the AnnotationSpec that had been identified.

**Type**

#### type_()

The type of the prediction. The requested types can be configured via parameters. This will be one of

- segment-classification
- shot-classification
one-sec-interval-classification

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end. Note that for ‘segment-classification’ prediction type, this equals the original ‘timeSegmentStart’ from the input instance, for other types it is the start of a shot or a 1 second interval respectively.

#### time_segment_end()

The end, exclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end. Note that for ‘segment-classification’ prediction type, this equals the original ‘timeSegmentEnd’ from the input instance, for other types it is the end of a shot or a 1 second interval respectively.

#### confidence()

The Model’s confidence in correction of this prediction, higher value means higher confidence.

#### confidence(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### display_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### time_segment_start(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### type_(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Video Object Tracking.

#### id()

The resource ID of the AnnotationSpec that had been identified.

**Type**

#### display_name()

The display name of the AnnotationSpec that had been identified.

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### time_segment_end()

The end, inclusive, of the video’s time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### confidence()

The Model’s confidence in correction of this prediction, higher value means higher confidence.

#### frames()

All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object.

**Type**MutableSequence[

[google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult.Frame](https://docs.cloud.google.com/python/docs/reference/aiplatform/prediction_v1/types_.md#google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult.Frame)]

*class* Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

#### time_offset()

A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### x_min()

The leftmost coordinate of the bounding box.

#### x_max()

The rightmost coordinate of the bounding box.

#### y_min()

The topmost coordinate of the bounding box.

#### y_max()

The bottommost coordinate of the bounding box.

#### time_offset(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### x_max(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### x_min(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### y_max(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### y_min(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### confidence(*: wrappers_pb2.FloatValu* )

#### display_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### frames(*: MutableSequence[[Frame](../prediction_v1/types*.md#google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult.Frame)_ )

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig -->

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognitionInputs.ModelType -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardsAsyncPager -->

# Class ListTensorboardsAsyncPager (1.134.0)

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

## Methods

### ListTensorboardsAsyncPager

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesAsyncPager -->

# Class FetchExamplesAsyncPager (1.134.0)

```
FetchExamplesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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


A pager for iterating through `fetch_examples`

requests.

This class thinly wraps an initial
[FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse) object, and
provides an `__aiter__`

method to iterate through its
`examples`

field.

If there are more pages, the `__aiter__`

method will make additional
`FetchExamples`

requests and continue to iterate
through the `examples`

field on the
corresponding responses.

All the usual [FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### FetchExamplesAsyncPager

```
FetchExamplesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager -->

# Class ListRagFilesAsyncPager (1.134.0)

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagFilesAsyncPager

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Execution -->

# Class Execution (1.134.0)

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Execution. |
`display_name` |
`str`
User provided display name of the Execution. May be up to 128 Unicode characters. |
`state` |
The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines) and the system does not prescribe or check the validity of state transitions. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Executions. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was last updated. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in `schema_title` to use.
Schema title and version is expected to be registered in
earlier Create Schema calls. And both are used together as
unique identifiers to identify schemas within the local
metadata store.
|
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Execution |

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


Describes the state of the Execution.

## Methods

### Execution

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationRequest -->

# Class GetModelEvaluationRequest (1.134.0)

`GetModelEvaluationRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModelEvaluation.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelEvaluation resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|

## Methods

### GetModelEvaluationRequest

`GetModelEvaluationRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.GetModelEvaluation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelOperationMetadata -->

# Class MutateDeployedModelOperationMetadata (1.134.0)

```
MutateDeployedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.MutateDeployedModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### MutateDeployedModelOperationMetadata

```
MutateDeployedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.MutateDeployedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluation.BiasConfig -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSavedQueryRequest -->

# Class DeleteSavedQueryRequest (1.134.0)

`DeleteSavedQueryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteSavedQuery.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the SavedQuery to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/savedQueries/{saved_query}`
|

## Methods

### DeleteSavedQueryRequest

`DeleteSavedQueryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteSavedQuery.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNasTrialDetailRequest -->

# Class GetNasTrialDetailRequest (1.134.0)

`GetNasTrialDetailRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasTrialDetail.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasTrialDetail resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}/nasTrialDetails/{nas_trial_detail}`
|

## Methods

### GetNasTrialDetailRequest

`GetNasTrialDetailRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasTrialDetail.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureOnlineStoreRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.Value -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchSpec -->

# Class TrajectoryInOrderMatchSpec (1.134.0)

`TrajectoryInOrderMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryInOrderMatch metric - returns 1 if tool calls in the reference trajectory appear in the predicted trajectory in the same order, else 0.

## Methods

### TrajectoryInOrderMatchSpec

`TrajectoryInOrderMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryInOrderMatch metric - returns 1 if tool calls in the reference trajectory appear in the predicted trajectory in the same order, else 0.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchInput -->

# Class ToolParameterKVMatchInput (1.134.0)

`ToolParameterKVMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool parameter key value match metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for tool parameter key value match metric. |
`instances` |
`MutableSequence[`
Required. Repeated tool parameter key value match instances. |

## Methods

### ToolParameterKVMatchInput

`ToolParameterKVMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool parameter key value match metric.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse -->

# Class ListIndexesResponse (1.134.0)

`ListIndexesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexService.ListIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`indexes` |
`MutableSequence[`
List of indexes in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListIndexesRequest.page_token to obtain that page. |

## Methods

### ListIndexesResponse

`ListIndexesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexService.ListIndexes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityInput -->

# Class QuestionAnsweringQualityInput (1.134.0)

```
QuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering quality score metric. |
`instance` |
Required. Question answering quality instance. |

## Methods

### QuestionAnsweringQualityInput

```
QuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering quality metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationHelpfulnessInstance -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsAsyncPager -->

# Class SearchDataItemsAsyncPager (1.134.0)

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchDataItemsAsyncPager

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitorsPager -->

# Class ListModelMonitorsPager (1.134.0)

```
ListModelMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
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


A pager for iterating through `list_model_monitors`

requests.

This class thinly wraps an initial
[ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_monitors`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelMonitors`

requests and continue to iterate
through the `model_monitors`

field on the
corresponding responses.

All the usual [ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitorsPager

```
ListModelMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineFailurePolicy -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsAsyncPager -->

# Class ListNasTrialDetailsAsyncPager (1.134.0)

```
ListNasTrialDetailsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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


A pager for iterating through `list_nas_trial_details`

requests.

This class thinly wraps an initial
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_trial_details`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasTrialDetails`

requests and continue to iterate
through the `nas_trial_details`

field on the
corresponding responses.

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasTrialDetailsAsyncPager

```
ListNasTrialDetailsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsPager -->

# Class ListFeatureGroupsPager (1.134.0)

```
ListFeatureGroupsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureGroupsPager

```
ListFeatureGroupsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesPager -->

# Class ListNotebookRuntimesPager (1.134.0)

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesPager

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionsAsyncPager -->

# Class ListModelVersionsAsyncPager (1.134.0)

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
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


A pager for iterating through `list_model_versions`

requests.

This class thinly wraps an initial
[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersions`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionsAsyncPager

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient -->

# Class IndexEndpointServiceClient (1.134.0)

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's IndexEndpoints.

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
`IndexEndpointServiceTransport` |
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

### IndexEndpointServiceClient

```
IndexEndpointServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index endpoint service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexEndpointServiceTransport,Callable[..., IndexEndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexEndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index_endpoint

```
create_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.CreateIndexEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
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


Creates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1beta1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointRequest.html)(
parent="parent_value",
index_endpoint=index_endpoint,
)
# Make the request
operation = client.[create_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_create_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.CreateIndexEndpoint. |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: |
`index_endpoint` |
Required. The IndexEndpoint to create. This corresponds to the |
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

### delete_index_endpoint

```
delete_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.DeleteIndexEndpointRequest,
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


Deletes an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_delete_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.DeleteIndexEndpoint. |
`name` |
`str`
Required. The name of the IndexEndpoint resource to be deleted. Format: |
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

### deploy_index

```
deploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.DeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.DeployedIndex
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


Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it. Only non-empty Indexes can be deployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_deploy_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1beta1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1beta1.[DeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[deploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_deploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.DeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be created within the IndexEndpoint. This corresponds to the |
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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
`IndexEndpointServiceClient` |
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

### get_index_endpoint

```
get_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.GetIndexEndpointRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
```


Gets an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_get_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.GetIndexEndpoint |
`name` |
`str`
Required. The name of the IndexEndpoint resource. Format: |
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
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_index_endpoints

```
list_index_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
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
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsPager
)
```


Lists IndexEndpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_index_endpoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListIndexEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_index_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_list_index_endpoints)(request=request)
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
The request object. Request message for IndexEndpointService.ListIndexEndpoints. |
`parent` |
`str`
Required. The resource name of the Location from which to list the IndexEndpoints. Format: |
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
Response message for IndexEndpointService.ListIndexEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### mutate_deployed_index

```
mutate_deployed_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.MutateDeployedIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.DeployedIndex
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


Update an existing DeployedIndex under an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_mutate_deployed_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1beta1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1beta1.[MutateDeployedIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[mutate_deployed_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_mutate_deployed_index)(request=request)
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
The request object. Request message for IndexEndpointService.MutateDeployedIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are |
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

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### parse_index_path

`parse_index_path(path: str) -> typing.Dict[str, str]`


Parses a index path into its component segments.

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

### undeploy_index

```
undeploy_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.UndeployIndexRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[str] = None,
deployed_index_id: typing.Optional[str] = None,
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


Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_undeploy_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UndeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index_id="deployed_index_id_value",
)
# Make the request
operation = client.[undeploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_undeploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.UndeployIndex. |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. This corresponds to the |
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

### update_index_endpoint

```
update_index_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.UpdateIndexEndpointRequest,
dict,
]
] = None,
*,
index_endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
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
) -> google.cloud.aiplatform_v1beta1.types.index_endpoint.IndexEndpoint
```


Updates an IndexEndpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1beta1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexEndpointRequest.html)(
index_endpoint=index_endpoint,
)
# Make the request
response = client.[update_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceClient_update_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexEndpointService.UpdateIndexEndpoint. |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See |
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
Indexes are deployed into it. An IndexEndpoint can have multiple DeployedIndexes. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardTimeSeriesDataResponse -->

# Class ReadTensorboardTimeSeriesDataResponse (1.134.0)

```
ReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardTimeSeriesData.

## Attribute |
|
|---|---|
Name |
Description |
`time_series_data` |
The returned time series data. |

## Methods

### ReadTensorboardTimeSeriesDataResponse

```
ReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.TuningResourceUsageAssessmentConfig -->

# Class TuningResourceUsageAssessmentConfig (1.134.0)

```
TuningResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning resource usage assessment.

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. The name of the model used for tuning. |

## Methods

### TuningResourceUsageAssessmentConfig

```
TuningResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning resource usage assessment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAISearch.DataStoreSpec -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesAsyncPager -->

# Class SearchFeaturesAsyncPager (1.134.0)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchFeaturesAsyncPager

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource -->

# Class MigratableResource (1.134.0)

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

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
`ml_engine_model_version` |
Output only. Represents one Version in ml.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_model` |
Output only. Represents one Model in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_dataset` |
Output only. Represents one Dataset in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`data_labeling_dataset` |
Output only. Represents one Dataset in datalabeling.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`last_migrate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the last migration attempt on this MigratableResource started. Will not be set if there's no migration attempt on this MigratableResource. |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MigratableResource was last updated. |

## Classes

### AutomlDataset

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

### AutomlModel

`AutomlModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Model in automl.googleapis.com.

### DataLabelingDataset

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.

### MlEngineModelVersion

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.

## Methods

### MigratableResource

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardRunsPager -->

# Class ListTensorboardRunsPager (1.134.0)

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
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
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse) object, and
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

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardRunsPager

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsPager -->

# Class ListIndexEndpointsPager (1.134.0)

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexEndpointsPager

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager -->

# Class ListFeatureViewsPager (1.134.0)

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewsPager

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateStudyRequest -->

# Class CreateStudyRequest (1.134.0)

`CreateStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CreateStudy.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: `projects/{project}/locations/{location}`
|
`study` |
Required. The Study configuration used to create the Study. |

## Methods

### CreateStudyRequest

`CreateStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CreateStudy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardRunsResponse -->

# Class BatchCreateTensorboardRunsResponse (1.134.0)

```
BatchCreateTensorboardRunsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardRuns.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard_runs` |
`MutableSequence[`
The created TensorboardRuns. |

## Methods

### BatchCreateTensorboardRunsResponse

```
BatchCreateTensorboardRunsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardRuns.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.Value -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource -->

# Class MigratableResource (1.134.0)

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

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
`ml_engine_model_version` |
Output only. Represents one Version in ml.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_model` |
Output only. Represents one Model in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_dataset` |
Output only. Represents one Dataset in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`data_labeling_dataset` |
Output only. Represents one Dataset in datalabeling.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`last_migrate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the last migration attempt on this MigratableResource started. Will not be set if there's no migration attempt on this MigratableResource. |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MigratableResource was last updated. |

## Classes

### AutomlDataset

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

### AutomlModel

`AutomlModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Model in automl.googleapis.com.

### DataLabelingDataset

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.

### MlEngineModelVersion

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.

## Methods

### MigratableResource

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOnlineStoreRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource.AutomlDataset -->

# Class AutomlDataset (1.134.0)

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Full resource name of automl Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
The Dataset's display name in automl.googleapis.com. |

## Methods

### AutomlDataset

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateScheduleRequest -->

# Class CreateScheduleRequest (1.134.0)

`CreateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.CreateSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Schedule in. Format: `projects/{project}/locations/{location}`
|
`schedule` |
Required. The Schedule to create. |

## Methods

### CreateScheduleRequest

`CreateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.CreateSchedule.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service -->

# Package data_foundry_service (1.134.0)

API documentation for `aiplatform_v1.services.data_foundry_service`

package.

## Classes

[DataFoundryServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient)

Service for generating and preparing datasets for Gen AI evaluation.

[DataFoundryServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient)

Service for generating and preparing datasets for Gen AI evaluation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateCachedContentRequest -->

# Class CreateCachedContentRequest (1.134.0)

`CreateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.CreateCachedContent.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent resource where the cached content will be created |
`cached_content` |
Required. The cached content to create |

## Methods

### CreateCachedContentRequest

`CreateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.CreateCachedContent.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationVerbositySpec -->

# Class SummarizationVerbositySpec (1.134.0)

`SummarizationVerbositySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization verbosity score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute summarization verbosity. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SummarizationVerbositySpec

`SummarizationVerbositySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization verbosity score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse -->

# Class ListAnnotationsResponse (1.134.0)

`ListAnnotationsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListAnnotations.

## Attributes |
|
|---|---|
Name |
Description |
`annotations` |
`MutableSequence[`
A list of Annotations that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListAnnotationsResponse

`ListAnnotationsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListAnnotations.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.DedicatedServingEndpoint -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessInstance -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LookupStudyRequest -->

# Class LookupStudyRequest (1.134.0)

`LookupStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.LookupStudy.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to get the Study from. Format: `projects/{project}/locations/{location}`
|
`display_name` |
`str`
Required. The user-defined display name of the Study |

## Methods

### LookupStudyRequest

`LookupStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.LookupStudy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardSizeRequest -->

# Class ReadTensorboardSizeRequest (1.134.0)

`ReadTensorboardSizeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ReadTensorboardSize.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard` |
`str`
Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### ReadTensorboardSizeRequest

`ReadTensorboardSizeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ReadTensorboardSize.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookExecutionJobRequest -->

# Class DeleteNotebookExecutionJobRequest (1.134.0)

```
DeleteNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.DeleteNotebookExecutionJob]

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource to be deleted. |

## Methods

### DeleteNotebookExecutionJobRequest

```
DeleteNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.DeleteNotebookExecutionJob]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateCustomJobRequest -->

# Class CreateCustomJobRequest (1.134.0)

`CreateCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CreateCustomJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: `projects/{project}/locations/{location}`
|
`custom_job` |
Required. The CustomJob to create. |

## Methods

### CreateCustomJobRequest

`CreateCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CreateCustomJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsPager -->

# Class ListPublisherModelsPager (1.134.0)

```
ListPublisherModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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


A pager for iterating through `list_publisher_models`

requests.

This class thinly wraps an initial
[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`publisher_models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPublisherModels`

requests and continue to iterate
through the `publisher_models`

field on the
corresponding responses.

All the usual [ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPublisherModelsPager

```
ListPublisherModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager -->

# Class ListTuningJobsAsyncPager (1.134.0)

```
ListTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTuningJobsAsyncPager

```
ListTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesPager -->

# Class ListReasoningEnginesPager (1.134.0)

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse) object, and
provides an `__iter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__iter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListReasoningEnginesPager

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchInput -->

# Class TrajectoryExactMatchInput (1.134.0)

`TrajectoryExactMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryExactMatch metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for TrajectoryExactMatch metric. |
`instances` |
`MutableSequence[`
Required. Repeated TrajectoryExactMatch instance. |

## Methods

### TrajectoryExactMatchInput

`TrajectoryExactMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryExactMatch metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetSpecialistPoolRequest -->

# Class GetSpecialistPoolRequest (1.134.0)

`GetSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.GetSpecialistPool.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the SpecialistPool resource. The form is `projects/{project}/locations/{location}/specialistPools/{specialist_pool}` .
|

## Methods

### GetSpecialistPoolRequest

`GetSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.GetSpecialistPool.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleDriveSource.ResourceId -->

# Class ResourceId (1.134.0)

`ResourceId(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type and ID of the Google Drive resource.

## Attributes |
|
|---|---|
Name |
Description |
`resource_type` |
Required. The type of the Google Drive resource. |
`resource_id` |
`str`
Required. The ID of the Google Drive resource. |

## Classes

### ResourceType

`ResourceType(value)`


The type of the Google Drive resource.

## Methods

### ResourceId

`ResourceId(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type and ID of the Google Drive resource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.BatchPredictionOutput -->

# Class BatchPredictionOutput (1.134.0)

`BatchPredictionOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Batch prediction job output.

## Attribute |
|
|---|---|
Name |
Description |
`batch_prediction_job` |
`str`
Vertex AI Batch prediction job resource name. The job must match the model version specified in [ModelMonitor].[model_monitoring_target]. |

## Methods

### BatchPredictionOutput

`BatchPredictionOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Batch prediction job output.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient -->

# Class ScheduleServiceClient (1.134.0)

```
ScheduleServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

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
`ScheduleServiceTransport` |
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

### ScheduleServiceClient

```
ScheduleServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the schedule service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ScheduleServiceTransport,Callable[..., ScheduleServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ScheduleServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_schedule

```
create_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.CreateScheduleRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
schedule: typing.Optional[
google.cloud.aiplatform_v1beta1.types.schedule.Schedule
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.schedule.Schedule
```


Creates a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1beta1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1beta1.[CreateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateScheduleRequest.html)(
parent="parent_value",
schedule=schedule,
)
# Make the request
response = client.[create_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_create_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.CreateSchedule. |
`parent` |
`str`
Required. The resource name of the Location to create the Schedule in. Format: |
`schedule` |
Required. The Schedule to create. This corresponds to the |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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

### delete_schedule

```
delete_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.DeleteScheduleRequest,
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


Deletes a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteScheduleRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_delete_schedule)(request=request)
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
The request object. Request message for ScheduleService.DeleteSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be deleted. Format: |
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
`ScheduleServiceClient` |
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
`ScheduleServiceClient` |
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
`ScheduleServiceClient` |
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

### get_schedule

```
get_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.GetScheduleRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.schedule.Schedule
```


Gets a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetScheduleRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_get_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.GetSchedule. |
`name` |
`str`
Required. The name of the Schedule resource. Format: |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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

### list_schedules

```
list_schedules(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
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
google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesPager
)
```


Lists Schedules in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_schedules():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSchedulesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_schedules](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_list_schedules)(request=request)
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
The request object. Request message for ScheduleService.ListSchedules. |
`parent` |
`str`
Required. The resource name of the Location to list the Schedules from. Format: |
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
Response message for ScheduleService.ListSchedules Iterating over this object will yield results and resolve additional pages automatically. |

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

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_model_monitor_path

`parse_model_monitor_path(path: str) -> typing.Dict[str, str]`


Parses a model_monitor path into its component segments.

### parse_model_monitoring_job_path

`parse_model_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_monitoring_job path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### pause_schedule

```
pause_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.PauseScheduleRequest,
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


Pauses a Schedule. Will mark xref_Schedule.state to 'PAUSED'. If the schedule is paused, no new runs will be created. Already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_pause_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[PauseScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseScheduleRequest.html)(
name="name_value",
)
# Make the request
client.[pause_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_pause_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.PauseSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_schedule

```
resume_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.ResumeScheduleRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
catch_up: typing.Optional[bool] = None,
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


Resumes a paused Schedule to start scheduling new runs. Will mark xref_Schedule.state to 'ACTIVE'. Only paused Schedule can be resumed.

When the Schedule is resumed, new runs will be scheduled starting from the next execution time after the current time based on the time_specification in the Schedule. If [Schedule.catchUp][] is set up true, all missed runs will be scheduled for backfill first.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_resume_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ResumeScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeScheduleRequest.html)(
name="name_value",
)
# Make the request
client.[resume_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_resume_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.ResumeSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: |
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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

### update_schedule

```
update_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.schedule_service.UpdateScheduleRequest,
dict,
]
] = None,
*,
schedule: typing.Optional[
google.cloud.aiplatform_v1beta1.types.schedule.Schedule
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
) -> google.cloud.aiplatform_v1beta1.types.schedule.Schedule
```


Updates an active or paused Schedule.

When the Schedule is updated, new runs will be scheduled starting from the updated next execution time after the update time based on the time_specification in the updated Schedule. All unstarted runs before the update time will be skipped while already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1beta1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1beta1.[UpdateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateScheduleRequest.html)(
schedule=schedule,
)
# Make the request
response = client.[update_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceClient_update_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.UpdateSchedule. |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresAsyncPager -->

# Class ListMetadataStoresAsyncPager (1.134.0)

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
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


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataStoresAsyncPager

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesAsyncPager -->

# Class ListSavedQueriesAsyncPager (1.134.0)

```
ListSavedQueriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
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


A pager for iterating through `list_saved_queries`

requests.

This class thinly wraps an initial
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`saved_queries`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSavedQueries`

requests and continue to iterate
through the `saved_queries`

field on the
corresponding responses.

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSavedQueriesAsyncPager

```
ListSavedQueriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebaseTunedModelOperationMetadata -->

# Class RebaseTunedModelOperationMetadata (1.134.0)

```
RebaseTunedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for GenAiTuningService.RebaseTunedModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation generic information. |

## Methods

### RebaseTunedModelOperationMetadata

```
RebaseTunedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for GenAiTuningService.RebaseTunedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SlackSource -->

# Class SlackSource (1.134.0)

`SlackSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Slack source for the ImportRagFilesRequest.

## Attribute |
|
|---|---|
Name |
Description |
`channels` |
`MutableSequence[`
Required. The Slack channels. |

## Classes

### SlackChannels

`SlackChannels(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannels contains the Slack channels and corresponding access token.

## Methods

### SlackSource

`SlackSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Slack source for the ImportRagFilesRequest.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchSpec -->

# Class TrajectoryAnyOrderMatchSpec (1.134.0)

`TrajectoryAnyOrderMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryAnyOrderMatch metric - returns 1 if all tool calls in the reference trajectory appear in the predicted trajectory in any order, else 0.

## Methods

### TrajectoryAnyOrderMatchSpec

`TrajectoryAnyOrderMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryAnyOrderMatch metric - returns 1 if all tool calls in the reference trajectory appear in the predicted trajectory in any order, else 0.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchInput -->

# Class ToolParameterKVMatchInput (1.134.0)

`ToolParameterKVMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool parameter key value match metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for tool parameter key value match metric. |
`instances` |
`MutableSequence[`
Required. Repeated tool parameter key value match instances. |

## Methods

### ToolParameterKVMatchInput

`ToolParameterKVMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for tool parameter key value match metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory -->

# Class Memory (1.134.0)

`Memory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory.

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
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what `expiration` was sent on input.
This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. Input only. The TTL for this resource. The expiration time is computed: now + TTL. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Identifier. The resource name of the Memory. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/memories/{memory}`
|
`display_name` |
`str`
Optional. Display name of the Memory. |
`description` |
`str`
Optional. Description of the Memory. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Memory was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Memory was most recently updated. |
`fact` |
`str`
Required. Semantic knowledge extracted from the source content. |
`scope` |
`MutableMapping[str, str]`
Required. Immutable. The scope of the Memory. Memories are isolated within their scope. The scope is defined when creating or generating memories. Scope values cannot contain the wildcard character '\*'. |

## Classes

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

## Methods

### Memory

`Memory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.DedicatedServingEndpoint -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelOperationMetadata -->

# Class MutateDeployedModelOperationMetadata (1.134.0)

```
MutateDeployedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.MutateDeployedModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### MutateDeployedModelOperationMetadata

```
MutateDeployedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.MutateDeployedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse -->

# Class ListSavedQueriesResponse (1.134.0)

`ListSavedQueriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListSavedQueries.

## Attributes |
|
|---|---|
Name |
Description |
`saved_queries` |
`MutableSequence[`
A list of SavedQueries that match the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListSavedQueriesResponse

`ListSavedQueriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListSavedQueries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager -->

# Class ListFeaturestoresAsyncPager (1.134.0)

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturestoresAsyncPager

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsAsyncPager -->

# Class ListDataLabelingJobsAsyncPager (1.134.0)

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse,
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


A pager for iterating through `list_data_labeling_jobs`

requests.

This class thinly wraps an initial
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_labeling_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDataLabelingJobs`

requests and continue to iterate
through the `data_labeling_jobs`

field on the
corresponding responses.

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataLabelingJobsAsyncPager

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReservationAffinity.Type -->

# Class Type (1.134.0)

`Type(value)`


Identifies a type of reservation affinity.

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Default value. This should not be used. |
`NO_RESERVATION` |
Do not consume from any reserved capacity, only use on-demand. |
`ANY_RESERVATION` |
Consume any reservation available, falling back to on-demand. |
`SPECIFIC_RESERVATION` |
Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

## Methods

### Type

`Type(value)`


Identifies a type of reservation affinity.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SyncFeatureViewRequest -->

# Class SyncFeatureViewRequest (1.134.0)

`SyncFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.SyncFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
Required. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### SyncFeatureViewRequest

`SyncFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.SyncFeatureView.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service -->

# Package match_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.match_service`

package.

## Classes

[MatchServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient)

MatchService is a Google managed service for efficient vector similarity search at scale.

[MatchServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient)

MatchService is a Google managed service for efficient vector similarity search at scale.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CopyModelResponse -->

# Class CopyModelResponse (1.134.0)

`CopyModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.CopyModel operation.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
The name of the copied Model resource. Format: `projects/{project}/locations/{location}/models/{model}`
|
`model_version_id` |
`str`
Output only. The version ID of the model that is copied. |

## Methods

### CopyModelResponse

`CopyModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.CopyModel operation.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager -->

# Class ListPipelineJobsAsyncPager (1.134.0)

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

## Methods

### ListPipelineJobsAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesPager -->

# Class ListTrainingPipelinesPager (1.134.0)

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

## Methods

### ListTrainingPipelinesPager

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MachineSpec -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTrainingPipelineRequest -->

# Class GetTrainingPipelineRequest (1.134.0)

`GetTrainingPipelineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline resource. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### GetTrainingPipelineRequest

`GetTrainingPipelineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardTimeSeriesDataResponse -->

# Class ReadTensorboardTimeSeriesDataResponse (1.134.0)

```
ReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardTimeSeriesData.

## Attribute |
|
|---|---|
Name |
Description |
`time_series_data` |
The returned time series data. |

## Methods

### ReadTensorboardTimeSeriesDataResponse

```
ReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest -->

# Class MigrateResourceRequest (1.134.0)

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`migrate_ml_engine_model_version_config` |
Config for migrating Version in ml.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_model_config` |
Config for migrating Model in automl.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_dataset_config` |
Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|
`migrate_data_labeling_dataset_config` |
Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|

## Classes

### MigrateAutomlDatasetConfig

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.

### MigrateAutomlModelConfig

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.

### MigrateDataLabelingDatasetConfig

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.

### MigrateMlEngineModelVersionConfig

```
MigrateMlEngineModelVersionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating version in ml.googleapis.com to Vertex AI's Model.

## Methods

### MigrateResourceRequest

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringQualityInstance -->

# Class QuestionAnsweringQualityInstance (1.134.0)

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

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
Required. Text to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Question Answering prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringQualityInstance

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource.AutomlDataset -->

# Class AutomlDataset (1.134.0)

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Full resource name of automl Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
The Dataset's display name in automl.googleapis.com. |

## Methods

### AutomlDataset

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.ComputerUse -->

# Class ComputerUse (1.134.0)

`ComputerUse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support computer use.

## Attributes |
|
|---|---|
Name |
Description |
`environment` |
Required. The environment being operated. |
`excluded_predefined_functions` |
`MutableSequence[str]`
Optional. By default, `predefined functions |

## Classes

### Environment

`Environment(value)`


Represents the environment being operated, such as a web browser.

## Methods

### ComputerUse

`ComputerUse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support computer use.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager -->

# Class ListDatasetVersionsAsyncPager (1.134.0)

```
ListDatasetVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDatasetVersions`

requests and continue to iterate
through the `dataset_versions`

field on the
corresponding responses.

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetVersionsAsyncPager

```
ListDatasetVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateStudyRequest -->

# Class CreateStudyRequest (1.134.0)

`CreateStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CreateStudy.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: `projects/{project}/locations/{location}`
|
`study` |
Required. The Study configuration used to create the Study. |

## Methods

### CreateStudyRequest

`CreateStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.CreateStudy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MultiSpeakerVoiceConfig -->

# Class MultiSpeakerVoiceConfig (1.134.0)

`MultiSpeakerVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a multi-speaker text-to-speech request.

## Attribute |
|
|---|---|
Name |
Description |
`speaker_voice_configs` |
`MutableSequence[`
Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided. |

## Methods

### MultiSpeakerVoiceConfig

`MultiSpeakerVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a multi-speaker text-to-speech request.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardSizeRequest -->

# Class ReadTensorboardSizeRequest (1.134.0)

`ReadTensorboardSizeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ReadTensorboardSize.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard` |
`str`
Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### ReadTensorboardSizeRequest

`ReadTensorboardSizeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ReadTensorboardSize.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LookupStudyRequest -->

# Class LookupStudyRequest (1.134.0)

`LookupStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.LookupStudy.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to get the Study from. Format: `projects/{project}/locations/{location}`
|
`display_name` |
`str`
Required. The user-defined display name of the Study |

## Methods

### LookupStudyRequest

`LookupStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.LookupStudy.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GoogleDriveSource -->

# Class GoogleDriveSource (1.134.0)

`GoogleDriveSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Drive location for the input content.

## Attribute |
|
|---|---|
Name |
Description |
`resource_ids` |
`MutableSequence[`
Required. Google Drive resource IDs. |

## Classes

### ResourceId

`ResourceId(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type and ID of the Google Drive resource.

## Methods

### GoogleDriveSource

`GoogleDriveSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Drive location for the input content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbositySpec -->

# Class SummarizationVerbositySpec (1.134.0)

`SummarizationVerbositySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization verbosity score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute summarization verbosity. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SummarizationVerbositySpec

`SummarizationVerbositySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization verbosity score metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateScheduleRequest -->

# Class CreateScheduleRequest (1.134.0)

`CreateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.CreateSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Schedule in. Format: `projects/{project}/locations/{location}`
|
`schedule` |
Required. The Schedule to create. |

## Methods

### CreateScheduleRequest

`CreateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.CreateSchedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCachedContentRequest -->

# Class CreateCachedContentRequest (1.134.0)

`CreateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.CreateCachedContent.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent resource where the cached content will be created |
`cached_content` |
Required. The cached content to create |

## Methods

### CreateCachedContentRequest

`CreateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.CreateCachedContent.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsPager -->

# Class ListBatchPredictionJobsPager (1.134.0)

```
ListBatchPredictionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListBatchPredictionJobsPager

```
ListBatchPredictionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest -->

# Class MigrateResourceRequest (1.134.0)

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`migrate_ml_engine_model_version_config` |
Config for migrating Version in ml.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_model_config` |
Config for migrating Model in automl.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_dataset_config` |
Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|
`migrate_data_labeling_dataset_config` |
Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|

## Classes

### MigrateAutomlDatasetConfig

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.

### MigrateAutomlModelConfig

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.

### MigrateDataLabelingDatasetConfig

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.

### MigrateMlEngineModelVersionConfig

```
MigrateMlEngineModelVersionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating version in ml.googleapis.com to Vertex AI's Model.

## Methods

### MigrateResourceRequest

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesAsyncPager -->

# Class ListEntityTypesAsyncPager (1.134.0)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesAsyncPager

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationsAsyncPager -->

# Class ListModelEvaluationsAsyncPager (1.134.0)

```
ListModelEvaluationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
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


A pager for iterating through `list_model_evaluations`

requests.

This class thinly wraps an initial
[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_evaluations`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelEvaluations`

requests and continue to iterate
through the `model_evaluations`

field on the
corresponding responses.

All the usual [ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationsAsyncPager

```
ListModelEvaluationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookExecutionJobRequest -->

# Class DeleteNotebookExecutionJobRequest (1.134.0)

```
DeleteNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.DeleteNotebookExecutionJob]

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource to be deleted. |

## Methods

### DeleteNotebookExecutionJobRequest

```
DeleteNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.DeleteNotebookExecutionJob]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelOperationMetadata -->

# Class RebaseTunedModelOperationMetadata (1.134.0)

```
RebaseTunedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for GenAiTuningService.RebaseTunedModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation generic information. |

## Methods

### RebaseTunedModelOperationMetadata

```
RebaseTunedModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for GenAiTuningService.RebaseTunedModel.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.CodeExecution -->

# Class CodeExecution (1.134.0)

`CodeExecution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output to this tool.

## Methods

### CodeExecution

`CodeExecution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output to this tool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCustomJobRequest -->

# Class CreateCustomJobRequest (1.134.0)

`CreateCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CreateCustomJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: `projects/{project}/locations/{location}`
|
`custom_job` |
Required. The CustomJob to create. |

## Methods

### CreateCustomJobRequest

`CreateCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CreateCustomJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager -->

# Class ListSpecialistPoolsPager (1.134.0)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsPager

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager -->

# Class ListRagCorporaAsyncPager (1.134.0)

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagCorporaAsyncPager

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasAsyncPager -->

# Class ListMetadataSchemasAsyncPager (1.134.0)

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataSchemasAsyncPager

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel -->

# Class DeployedModel (1.134.0)

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

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
`id` |
`str`
Immutable. The ID of the DeployedModel. If not provided upon deployment, Vertex AI will generate a value for this ID. This value should be 1-10 characters, and valid characters are `/[0-9]/` .
|
`model` |
`str`
The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint. The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
if no version is specified, the default version will be
deployed.
|
`model_version_id` |
`str`
Output only. The version ID of the model that is deployed. |
`display_name` |
`str`
The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedModel was created. |
`explanation_spec` |
Explanation configuration for this DeployedModel. When deploying a Model using EndpointService.DeployModel, this value overrides the value of Model.explanation_spec. All fields of explanation_spec are optional in the request. If a field of explanation_spec is not populated, the value of the same field of Model.explanation_spec is inherited. If the corresponding Model.explanation_spec is not populated, all fields of the explanation_spec will be used for the explanation configuration. |
`disable_explanations` |
`bool`
If true, deploy the model without explainable feature, regardless the existence of Model.explanation_spec or explanation_spec. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`disable_container_logging` |
`bool`
For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`enable_access_logging` |
`bool`
If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request. Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`private_endpoints` |
Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if network is configured. |
`faster_deployment_config` |
Configuration for faster model deployment. |
`status` |
Output only. Runtime status of the deployed model. |
`system_labels` |
`MutableMapping[str, str]`
System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`checkpoint_id` |
`str`
The checkpoint id of the model. |
`speculative_decoding_spec` |
Optional. Spec for configuring speculative decoding. |

## Classes

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

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

## Methods

### DeployedModel

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationSlicesPager -->

# Class ListModelEvaluationSlicesPager (1.134.0)

```
ListModelEvaluationSlicesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
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


A pager for iterating through `list_model_evaluation_slices`

requests.

This class thinly wraps an initial
[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse) object, and
provides an `__iter__`

method to iterate through its
`model_evaluation_slices`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelEvaluationSlices`

requests and continue to iterate
through the `model_evaluation_slices`

field on the
corresponding responses.

All the usual [ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationSlicesPager

```
ListModelEvaluationSlicesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.VertexRagStore -->

# Class VertexRagStore (1.134.0)

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_resources` |
`MutableSequence[`
Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support. |
`vector_distance_threshold` |
`float`
Optional. Only return contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `_vector_distance_threshold` .
|

## Classes

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Methods

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSpecialistPoolRequest -->

# Class GetSpecialistPoolRequest (1.134.0)

`GetSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.GetSpecialistPool.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the SpecialistPool resource. The form is `projects/{project}/locations/{location}/specialistPools/{specialist_pool}` .
|

## Methods

### GetSpecialistPoolRequest

`GetSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.GetSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateReasoningEngineOperationMetadata -->

# Class UpdateReasoningEngineOperationMetadata (1.134.0)

```
UpdateReasoningEngineOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ReasoningEngineService.UpdateReasoningEngine operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateReasoningEngineOperationMetadata

```
UpdateReasoningEngineOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ReasoningEngineService.UpdateReasoningEngine operation.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityInstance -->

# Class QuestionAnsweringQualityInstance (1.134.0)

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

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
Required. Text to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Question Answering prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringQualityInstance

```
QuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJobDetail -->

# Class PipelineJobDetail (1.134.0)

`PipelineJobDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of PipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`pipeline_context` |
Output only. The context of the pipeline. |
`pipeline_run_context` |
Output only. The context of the current pipeline run. |
`task_details` |
`MutableSequence[`
Output only. The runtime details of the tasks under the pipeline. |

## Methods

### PipelineJobDetail

`PipelineJobDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of PipelineJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetReasoningEngineRequest -->

# Class GetReasoningEngineRequest (1.134.0)

`GetReasoningEngineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.GetReasoningEngine.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|

## Methods

### GetReasoningEngineRequest

`GetReasoningEngineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ReasoningEngineService.GetReasoningEngine.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagEmbeddingModelConfig -->

# Class RagEmbeddingModelConfig (1.134.0)

`RagEmbeddingModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the embedding model to use for RAG.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`vertex_prediction_endpoint` |
The Vertex AI Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. Endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search. This field is a member of `oneof` _ `model_config` .
|

## Classes

### VertexPredictionEndpoint

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

## Methods

### RagEmbeddingModelConfig

`RagEmbeddingModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the embedding model to use for RAG.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexEndpointOperationMetadata -->

# Class CreateIndexEndpointOperationMetadata (1.134.0)

```
CreateIndexEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.CreateIndexEndpoint.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateIndexEndpointOperationMetadata

```
CreateIndexEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.CreateIndexEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageRequest -->

# Class ReadTensorboardUsageRequest (1.134.0)

`ReadTensorboardUsageRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ReadTensorboardUsage.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard` |
`str`
Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### ReadTensorboardUsageRequest

`ReadTensorboardUsageRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ReadTensorboardUsage.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsPager -->

# Class ListFeatureMonitorsPager (1.134.0)

```
ListFeatureMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
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


A pager for iterating through `list_feature_monitors`

requests.

This class thinly wraps an initial
[ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_monitors`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureMonitors`

requests and continue to iterate
through the `feature_monitors`

field on the
corresponding responses.

All the usual [ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureMonitorsPager

```
ListFeatureMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardsAsyncPager -->

# Class ListTensorboardsAsyncPager (1.134.0)

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
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
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse) object, and
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

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardsAsyncPager

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
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
