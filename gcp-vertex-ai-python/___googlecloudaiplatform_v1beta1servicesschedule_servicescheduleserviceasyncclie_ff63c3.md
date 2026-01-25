---
merged_at: 2026-01-25T21:47:44.379904
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesschedule_servicescheduleserviceasyncclien_39eceb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesschedule_servicescheduleserviceasyncclient_056ad1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesschedule_servicescheduleserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient -->

# Class ScheduleServiceAsyncClient (1.134.0)

```
ScheduleServiceAsyncClient(
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
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport,
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_create_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
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
response = await client.[create_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_create_schedule)(request=request)
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
google.cloud.aiplatform_v1beta1.types.schedule_service.DeleteScheduleRequest,
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
from google.cloud import aiplatform_v1beta1
async def sample_delete_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteScheduleRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_delete_schedule)(request=request)
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
google.cloud.aiplatform_v1beta1.types.schedule_service.GetScheduleRequest,
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
async def sample_get_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetScheduleRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_get_schedule)(request=request)
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
google.cloud.aiplatform_v1beta1.services.schedule_service.transports.base.ScheduleServiceTransport
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
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
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
google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesAsyncPager
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
async def sample_list_schedules():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSchedulesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_schedules](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_list_schedules)(request=request)
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
from google.cloud import aiplatform_v1beta1
async def sample_pause_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[PauseScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseScheduleRequest.html)(
name="name_value",
)
# Make the request
await client.[pause_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_pause_schedule)(request=request)


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
google.cloud.aiplatform_v1beta1.types.schedule_service.ResumeScheduleRequest,
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
async def sample_resume_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ResumeScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeScheduleRequest.html)(
name="name_value",
)
# Make the request
await client.[resume_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_resume_schedule)(request=request)


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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_update_schedule():
# Create a client
client = aiplatform_v1beta1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html)()
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
response = await client.[update_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_schedule_service_ScheduleServiceAsyncClient_update_schedule)(request=request)
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_endpoint_serviceindexendpointserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient -->

# Class IndexEndpointServiceAsyncClient (1.134.0)

```
IndexEndpointServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### IndexEndpointServiceAsyncClient

```
IndexEndpointServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index endpoint service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexEndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1beta1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointRequest.html)(
parent="parent_value",
index_endpoint=index_endpoint,
)
# Make the request
operation = client.[create_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_create_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.CreateIndexEndpoint. |
`parent` |
Required. The resource name of the Location to create the IndexEndpoint in. Format: |
`index_endpoint` |
Required. The IndexEndpoint to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_delete_index_endpoint)(request=request)
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
The request object. Request message for IndexEndpointService.DeleteIndexEndpoint. |
`name` |
Required. The name of the IndexEndpoint resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_deploy_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1beta1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1beta1.[DeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[deploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_deploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.DeployIndex. |
`index_endpoint` |
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be created within the IndexEndpoint. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`IndexEndpointServiceAsyncClient` |
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
`IndexEndpointServiceAsyncClient` |
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
`IndexEndpointServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexEndpointRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_get_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexEndpointService.GetIndexEndpoint |
`name` |
Required. The name of the IndexEndpoint resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.transports.base.IndexEndpointServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsAsyncPager
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
async def sample_list_index_endpoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListIndexEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_index_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_list_index_endpoints)(request=request)
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
The request object. Request message for IndexEndpointService.ListIndexEndpoints. |
`parent` |
Required. The resource name of the Location from which to list the IndexEndpoints. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_mutate_deployed_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_index = aiplatform_v1beta1.[DeployedIndex](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndex.html)()
deployed_index.id = "id_value"
deployed_index.index = "index_value"
request = aiplatform_v1beta1.[MutateDeployedIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index=deployed_index,
)
# Make the request
operation = client.[mutate_deployed_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_mutate_deployed_index)(request=request)
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
The request object. Request message for IndexEndpointService.MutateDeployedIndex. |
`index_endpoint` |
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: |
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_undeploy_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UndeployIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexRequest.html)(
index_endpoint="index_endpoint_value",
deployed_index_id="deployed_index_id_value",
)
# Make the request
operation = client.[undeploy_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_undeploy_index)(request=request)
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
The request object. Request message for IndexEndpointService.UndeployIndex. |
`index_endpoint` |
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: |
`deployed_index_id` |
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_update_index_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[IndexEndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html)()
# Initialize request argument(s)
index_endpoint = aiplatform_v1beta1.[IndexEndpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexEndpoint.html)()
index_endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateIndexEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexEndpointRequest.html)(
index_endpoint=index_endpoint,
)
# Make the request
response = await client.[update_index_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.IndexEndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_endpoint_service_IndexEndpointServiceAsyncClient_update_index_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexEndpointService.UpdateIndexEndpoint. |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. This corresponds to the |
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatformv1schematrainingjobdefinition_v1types___googlecloudaipl_83be57.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1schematrainingjobdefinition_v1types___googlecloudaipla_8ab178.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schematrainingjobdefinition_v1types___googlecloudaiplat_7d33fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1types___googlecloudaiplatf_2140f7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types -->

# Package definition_v1.types (1.134.0)

API documentation for `definition_v1.types`

package.

## Classes

[AutoMlImageClassification](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassification)

A TrainingJob that trains and uploads an AutoML Image Classification Model.

[AutoMlImageClassificationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs)

[AutoMlImageClassificationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata)

[AutoMlImageObjectDetection](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetection)

A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

[AutoMlImageObjectDetectionInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs)

[AutoMlImageObjectDetectionMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata)

[AutoMlImageSegmentation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentation)

A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

[AutoMlImageSegmentationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs)

[AutoMlImageSegmentationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata)

[AutoMlTables](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTables)

A TrainingJob that trains and uploads an AutoML Tables Model.

[AutoMlTablesInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs)

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AutoMlTablesMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata)

Model metadata specific to AutoML Tables.

[AutoMlTextClassification](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassification)

A TrainingJob that trains and uploads an AutoML Text Classification Model.

[AutoMlTextClassificationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs)

[AutoMlTextExtraction](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtraction)

A TrainingJob that trains and uploads an AutoML Text Extraction Model.

[AutoMlTextExtractionInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs)

API documentation for `aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs`

class.

[AutoMlTextSentiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentiment)

A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

[AutoMlTextSentimentInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentimentInputs)

[AutoMlVideoActionRecognition](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognition)

A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

[AutoMlVideoActionRecognitionInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs)

[AutoMlVideoClassification](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassification)

A TrainingJob that trains and uploads an AutoML Video Classification Model.

[AutoMlVideoClassificationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs)

[AutoMlVideoObjectTracking](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTracking)

A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

[AutoMlVideoObjectTrackingInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs)

[ExportEvaluatedDataItemsConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig)

Configuration for exporting test set predictions to a BigQuery table.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespipelinetaskdetailoutputsentry_googlecloudai_58a729.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinetaskdetailoutputsentry_googlecloudaip_d8186b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskdetailoutputsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskDetail.OutputsEntry -->

# Class OutputsEntry (1.134.0)

`OutputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### OutputsEntry

`OutputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelopensourcecategory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.OpenSourceCategory -->

# Class OpenSourceCategory (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfluencyresult_googlecloudaiplatform_v1typesstreamq_b2226a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfluencyresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FluencyResult -->

# Class FluencyResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamqueryreasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamQueryReasoningEngineRequest -->

# Class StreamQueryReasoningEngineRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeswritetensorboardrundatarequest_googleclouda_89366d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeswritetensorboardrundatarequest_googlecloudai_c29f3f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeswritetensorboardrundatarequest_googlecloudaip_682fea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeswritetensorboardrundatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardRunDataRequest -->

# Class WriteTensorboardRunDataRequest (1.134.0)

```
WriteTensorboardRunDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardRunData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_run` |
`str`
Required. The resource name of the TensorboardRun to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|
`time_series_data` |
`MutableSequence[`
Required. The TensorboardTimeSeries data to write. Values with in a time series are indexed by their step value. Repeated writes to the same step will overwrite the existing value for that step. The upper limit of data points per write request is 5000. |

## Methods

### WriteTensorboardRunDataRequest

```
WriteTensorboardRunDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardRunData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigratableresourcedatalabelingdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource.DataLabelingDataset -->

# Class DataLabelingDataset (1.134.0)

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Full resource name of data labeling Dataset. Format: `projects/{project}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
The Dataset's display name in datalabeling.googleapis.com. |
`data_labeling_annotated_datasets` |
`MutableSequence[`
The migratable AnnotatedDataset in datalabeling.googleapis.com belongs to the data labeling Dataset. |

## Classes

### DataLabelingAnnotatedDataset

```
DataLabelingAnnotatedDataset(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents one AnnotatedDataset in datalabeling.googleapis.com.

## Methods

### DataLabelingDataset

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragmanageddbconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig -->

# Class RagManagedDbConfig (1.134.0)

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

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
`scaled` |
Sets the RagManagedDb to the Scaled tier. This field is a member of `oneof` _ `tier` .
|
`basic` |
Sets the RagManagedDb to the Basic tier. This field is a member of `oneof` _ `tier` .
|
`unprovisioned` |
Sets the RagManagedDb to the Unprovisioned tier. This field is a member of `oneof` _ `tier` .
|

## Classes

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### RagManagedDbConfig

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesbatchpredictionjoblabelsentry_googlecloudaip_5cb4dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbatchpredictionjoblabelsentry_googlecloudaipl_60865f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchpredictionjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesrequestscopeentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.ScopeEntry -->

# Class ScopeEntry (1.134.0)

`ScopeEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquerydeployedmodelsrequest_googlecloudaiplatf_2dfddb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquerydeployedmodelsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsRequest -->

# Class QueryDeployedModelsRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessharepointsources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SharePointSources -->

# Class SharePointSources (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequestfullexport_googl_57bc0b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequestfullexport_google_26c328.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequestfullexport_googlec_ebe3fe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequestfullexport_googlecl_4ee6ef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportfeaturevaluesrequestfullexport.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest.FullExport -->

# Class FullExport (1.134.0)

`FullExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting all historical Feature values of all entities of the EntityType between [start_time, end_time].

## Attributes |
|
|---|---|
Name |
Description |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Excludes Feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in Feature Store. Timestamp, if present, must not have higher than millisecond precision. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Exports Feature values as of this timestamp. If not set, retrieve values as of now. Timestamp, if present, must not have higher than millisecond precision. |

## Methods

### FullExport

`FullExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting all historical Feature values of all entities of the EntityType between [start_time, end_time].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeswritetensorboardrundatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardRunDataRequest -->

# Class WriteTensorboardRunDataRequest (1.134.0)

```
WriteTensorboardRunDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardRunData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_run` |
`str`
Required. The resource name of the TensorboardRun to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|
`time_series_data` |
`MutableSequence[`
Required. The TensorboardTimeSeries data to write. Values with in a time series are indexed by their step value. Repeated writes to the same step will overwrite the existing value for that step. The upper limit of data points per write request is 5000. |

## Methods

### WriteTensorboardRunDataRequest

```
WriteTensorboardRunDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardRunData.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratecontentrequestlabelsentry_googlecloud_38a5b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratecontentrequestlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatepersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePersistentResourceRequest -->

# Class CreatePersistentResourceRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsrequest_googleclou_7afbea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsrequest_googlecloud_fc06cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsRequest -->

# Class SearchModelMonitoringStatsRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesannotationspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AnnotationSpec -->

# Class AnnotationSpec (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmigratableresourcedatalabelingdataset_googleclouda_495701.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigratableresourcedatalabelingdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource.DataLabelingDataset -->

# Class DataLabelingDataset (1.134.0)

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Full resource name of data labeling Dataset. Format: `projects/{project}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
The Dataset's display name in datalabeling.googleapis.com. |
`data_labeling_annotated_datasets` |
`MutableSequence[`
The migratable AnnotatedDataset in datalabeling.googleapis.com belongs to the data labeling Dataset. |

## Classes

### DataLabelingAnnotatedDataset

```
DataLabelingAnnotatedDataset(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents one AnnotatedDataset in datalabeling.googleapis.com.

## Methods

### DataLabelingDataset

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typestrajectoryexactmatchmetricvalue_googlecloud_dc0caa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typestrajectoryexactmatchmetricvalue_googleclouda_1c8407.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectoryexactmatchmetricvalue_googlecloudai_051f30.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryexactmatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchMetricValue -->

# Class TrajectoryExactMatchMetricValue (1.134.0)

```
TrajectoryExactMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryExactMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. TrajectoryExactMatch score. This field is a member of `oneof` _ `_score` .
|

## Methods

### TrajectoryExactMatchMetricValue

```
TrajectoryExactMatchMetricValue(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


TrajectoryExactMatch metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardexperimentlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardExperiment.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfullfinetunedresources_googlecloudaiplatform__28780e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfullfinetunedresources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FullFineTunedResources -->

# Class FullFineTunedResources (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescometresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometResult -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_service_google_244eee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_service_googlec_c8998d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service -->

# Package feature_online_store_admin_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.feature_online_store_admin_service`

package.

## Classes

[FeatureOnlineStoreAdminServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceAsyncClient)

The service that handles CRUD and List for resources for FeatureOnlineStore.

[FeatureOnlineStoreAdminServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient)

The service that handles CRUD and List for resources for FeatureOnlineStore.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers)

API documentation for `aiplatform_v1beta1.services.feature_online_store_admin_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupsertdatapointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpsertDatapointsRequest -->

# Class UpsertDatapointsRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupsertdatapointsrequest_googlecloudaiplatform_296a76.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupsertdatapointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsRequest -->

# Class UpsertDatapointsRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesindexdatapointcrowdingtag.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint.CrowdingTag -->

# Class CrowdingTag (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typestrialwebaccessurisentry_googlecloudaiplatform__db1530.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typestrialwebaccessurisentry_googlecloudaiplatform_v_a2c2be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestrialwebaccessurisentry_googlecloudaiplatform_v1_741be4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestrialwebaccessurisentry_googlecloudaiplatform_v1b_984814.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestrialwebaccessurisentry_googlecloudaiplatform_v1be_b5c8a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrialwebaccessurisentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial.WebAccessUrisEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesruntimeartifactpropertiesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact.PropertiesEntry -->

# Class PropertiesEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesresourceruntimeaccessurisentry_googlecloudaip_f9ca52.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesresourceruntimeaccessurisentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourceRuntime.AccessUrisEntry -->

# Class AccessUrisEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessharepointsources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SharePointSources -->

# Class SharePointSources (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelcontainerspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelContainerSpec -->

# Class ModelContainerSpec (1.134.0)

`ModelContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a container for serving predictions. Some fields in
this message correspond to fields in the ```
Kubernetes Container v1
core
specification <https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core>
```

__.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. Immutable. URI of the Docker image to be used as the custom container for serving predictions. This URI must identify an image in Artifact Registry or Container Registry. Learn more about the `container publishing requirements |
`command` |
`MutableSequence[str]`
Immutable. Specifies the command that runs when the container starts. This overrides the container's `ENTRYPOINT ` __.
Specify this field as an array of executable and arguments,
similar to a Docker `ENTRYPOINT` 's "exec" form, not its
"shell" form.
If you do not specify this field, then the container's
`ENTRYPOINT` runs, in conjunction with the
args
field or the container's
```CMD` ` ` __,
if either exists. If this field is not specified and the
container does not have an `ENTRYPOINT` , then refer to the
Docker documentation about `how ` CMD` and ` ENTRYPOINT`
interact |
`args` |
`MutableSequence[str]`
Immutable. Specifies arguments for the command that runs when the container starts. This overrides the container's CMD` ` ` __
and `CMD` determine what runs based on their default
behavior. See the Docker documentation about `how ` CMD`
and `ENTRYPOINT`
interact |
`env` |
`MutableSequence[`
Immutable. List of environment variables to set in the container. After the container starts running, code running in the container can read these environment variables. Additionally, the command and args fields can reference these variables. Later entries in this list can also reference earlier entries. For example, the following example sets the variable `VAR_2` to have the
value `foo bar` :
.. code:: json
[
{
"name": "VAR_1",
"value": "foo"
},
{
"name": "VAR_2",
"value": "$(VAR_1) bar"
}
]
If you switch the order of the variables in the example,
then the expansion does not occur.
This field corresponds to the `env` field of the
Kubernetes Containers `v1 core
API |
`ports` |
`MutableSequence[`
Immutable. List of ports to expose from the container. Vertex AI sends any prediction requests that it receives to the first port on this list. Vertex AI also sends `liveness and health checks |
`predict_route` |
`str`
Immutable. HTTP path on the container to send prediction requests to. Vertex AI forwards requests sent using projects.locations.endpoints.predict to this path on the container's IP address and port. Vertex AI then returns the container's response in the API response. For example, if you set this field to `/foo` , then when
Vertex AI receives a prediction request, it forwards the
request body in a POST request to the `/foo` path on the
port of your container specified by the first value of this
`ModelContainerSpec` 's
ports
field.
If you don't specify this field, it defaults to the
following value when you [deploy this Model to an
Endpoint][google.cloud.aiplatform.v1beta1.EndpointService.DeployModel]:
/v1/endpoints/ENDPOINT/deployedModels/DEPLOYED_MODEL:predict
The placeholders in this value are replaced as follows:
- ENDPOINT: The last segment (following `endpoints/` )of
the Endpoint.name][] field of the Endpoint where this
Model has been deployed. (Vertex AI makes this value
available to your container code as the
AIP_ENDPOINT_ID`` environment variable |
`health_route` |
`str`
Immutable. HTTP path on the container to send health checks to. Vertex AI intermittently sends GET requests to this path on the container's IP address and port to check that the container is healthy. Read more about `health checks |
`invoke_route_prefix` |
`str`
Immutable. Invoke route prefix for the custom container. "/\*" is the only supported value right now. By setting this field, any non-root route on this model will be accessible with [PredictionService.Invoke] eg: "/invoke/foo/bar". Only one of `predict_route` or `invoke_route_prefix` can
be set, and we default to using `predict_route` if this
field is not set. If this field is set, the Model can only
be deployed to dedicated endpoint.
|
`grpc_ports` |
`MutableSequence[`
Immutable. List of ports to expose from the container. Vertex AI sends gRPC prediction requests that it receives to the first port on this list. Vertex AI also sends liveness and health checks to this port. If you do not specify this field, gRPC requests to the container will be disabled. Vertex AI does not use ports other than the first one listed. This field corresponds to the `ports` field of the
Kubernetes Containers v1 core API.
|
`deployment_timeout` |
`google.protobuf.duration_pb2.Duration`
Immutable. Deployment timeout. Limit for deployment timeout is 2 hours. |
`shared_memory_size_mb` |
`int`
Immutable. The amount of the VM memory to reserve as the shared memory for the model in megabytes. |
`startup_probe` |
Immutable. Specification for Kubernetes startup probe. |
`health_probe` |
Immutable. Specification for Kubernetes readiness probe. |
`liveness_probe` |
Immutable. Specification for Kubernetes liveness probe. |

## Methods

### ModelContainerSpec

`ModelContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a container for serving predictions. Some fields in
this message correspond to fields in the ```
Kubernetes Container v1
core
specification <https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core>
```

__.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeshyperparametertuningjoblabelsentry_googlecl_7fb72f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeshyperparametertuningjoblabelsentry_googleclo_305654.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeshyperparametertuningjoblabelsentry_googleclou_2c45c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeshyperparametertuningjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HyperparameterTuningJob.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadataoutputsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.OutputsEntry -->

# Class OutputsEntry (1.134.0)

`OutputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### OutputsEntry

`OutputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolparameterkeymatchmetricvalue_googlecloudaiplat_ff1667.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkeymatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKeyMatchMetricValue -->

# Class ToolParameterKeyMatchMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesendpointtrafficsplitentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.TrafficSplitEntry -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistcachedcontentsrequest_googlecloudaiplatform_v_f0a1cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistcachedcontentsrequest_googlecloudaiplatform_v1_07d44b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistcachedcontentsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexamplestore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentmonitoringjoblabelsentry_googleclou_e5767d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookruntimetemplatelabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeTemplate.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesfeaturemonitoringstatsanomaly_googlecloudaiplat_b65682.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeaturemonitoringstatsanomaly_googlecloudaiplatf_2190f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeaturemonitoringstatsanomaly_googlecloudaiplatfo_08e5d5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturemonitoringstatsanomaly_googlecloudaiplatfor_658124.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturemonitoringstatsanomaly.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Feature.MonitoringStatsAnomaly -->

# Class MonitoringStatsAnomaly (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewvertexragsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VertexRagSource -->

# Class VertexRagSource (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescustomjobwebaccessurisentry_googlecloudaiplatform__8ba08e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescustomjobwebaccessurisentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJob.WebAccessUrisEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessupervisedtuningspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SupervisedTuningSpec -->

# Class SupervisedTuningSpec (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfluencyresult_googlecloudaiplatform_v1beta1t_015fbf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfluencyresult_googlecloudaiplatform_v1beta1ty_34d21a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfluencyresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencyResult -->

# Class FluencyResult (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrialwebaccessurisentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial.WebAccessUrisEntry -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatepersistentresourcerequest_googlecloudai_c034b5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatepersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceRequest -->

# Class CreatePersistentResourceRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespredictrequestresponseloggingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictRequestResponseLoggingConfig -->

# Class PredictRequestResponseLoggingConfig (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestuningjob___googlecloudaiplatform_v1typesnote_34a17e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestuningjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningJob -->

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
`distillation_spec` |
Tuning Spec for Distillation. This field is a member of `oneof` _ `tuning_spec` .
|
`partner_model_tuning_spec` |
Tuning Spec for open sourced and third party Partner models. This field is a member of `oneof` _ `tuning_spec` .
|
`veo_tuning_spec` |
Tuning Spec for Veo Tuning. This field is a member of `oneof` _ `tuning_spec` .
|
`name` |
`str`
Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|
`tuned_model_display_name` |
`str`
Optional. The display name of the TunedModel. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the TuningJob. |
`custom_base_model` |
`str`
Optional. The user-provided path to custom model weights. Set this field to tune a custom model. The path must be a Cloud Storage directory that contains the model weights in .safetensors format along with associated model metadata files. If this field is set, the base_model field must still be set to indicate which base model the custom model is derived from. This feature is only available for open source models. |
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
`pipeline_job` |
`str`
Output only. The resource name of the PipelineJob associated with the TuningJob. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}` .
|
`encryption_spec` |
Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key. |
`service_account` |
`str`
The service account that the tuningJob workload runs as. If not specified, the Vertex AI Secure Fine-Tuned Service Agent in the project will be used. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`output_uri` |
`str`
Optional. Cloud Storage path to the directory where tuning job outputs are written to. This field is only available and required for open source models. |
`evaluate_dataset_runs` |
`MutableSequence[`
Output only. Evaluation runs for the Tuning Job. |

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnotebookruntimeruntimestate_googlecloudaiplatform_d51833.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnotebookruntimeruntimestate_googlecloudaiplatform__f080aa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookruntimeruntimestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime.RuntimeState -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeseventactionsartifactdeltaentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventActions.ArtifactDeltaEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest -->

# Class DeleteFeatureValuesRequest (1.134.0)

`DeleteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeatureValues.

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
`select_entity` |
Select feature values to be deleted by specifying entities. This field is a member of `oneof` _ `DeleteOption` .
|
`select_time_range_and_feature` |
Select feature values to be deleted by specifying time range and features. This field is a member of `oneof` _ `DeleteOption` .
|
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`
|

## Classes

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.

## Methods

### DeleteFeatureValuesRequest

`DeleteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v_04a438.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v1_eb47b1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v1b_2cde6f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v1be_042a7c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v1bet_e304d9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v1beta_106d33.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescompletetrialrequest_googlecloudaiplatform_v1beta1_c8458d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescompletetrialrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CompleteTrialRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployedmodelsystemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.SystemLabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectoryinordermatchmetricvalue_googlecloud_5a3842.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryinordermatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchMetricValue -->

# Class TrajectoryInOrderMatchMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployedmodelsystemlabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.SystemLabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluateinstancesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateInstancesResponse -->

# Class EvaluateInstancesResponse (1.134.0)

`EvaluateInstancesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EvaluationService.EvaluateInstances.

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
`exact_match_results` |
Auto metric evaluation results. Results for exact match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`bleu_results` |
Results for bleu metric. This field is a member of `oneof` _ `evaluation_results` .
|
`rouge_results` |
Results for rouge metric. This field is a member of `oneof` _ `evaluation_results` .
|
`fluency_result` |
LLM-based metric evaluation result. General text generation metrics, applicable to other categories. Result for fluency metric. This field is a member of `oneof` _ `evaluation_results` .
|
`coherence_result` |
Result for coherence metric. This field is a member of `oneof` _ `evaluation_results` .
|
`safety_result` |
Result for safety metric. This field is a member of `oneof` _ `evaluation_results` .
|
`groundedness_result` |
Result for groundedness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`fulfillment_result` |
Result for fulfillment metric. This field is a member of `oneof` _ `evaluation_results` .
|
`summarization_quality_result` |
Summarization only metrics. Result for summarization quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pairwise_summarization_quality_result` |
Result for pairwise summarization quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`summarization_helpfulness_result` |
Result for summarization helpfulness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`summarization_verbosity_result` |
Result for summarization verbosity metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_quality_result` |
Question answering only metrics. Result for question answering quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pairwise_question_answering_quality_result` |
Result for pairwise question answering quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_relevance_result` |
Result for question answering relevance metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_helpfulness_result` |
Result for question answering helpfulness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_correctness_result` |
Result for question answering correctness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pointwise_metric_result` |
Generic metrics. Result for pointwise metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pairwise_metric_result` |
Result for pairwise metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_call_valid_results` |
Tool call metrics. Results for tool call valid metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_name_match_results` |
Results for tool name match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_parameter_key_match_results` |
Results for tool parameter key match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_parameter_kv_match_results` |
Results for tool parameter key value match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`comet_result` |
Translation metrics. Result for Comet metric. This field is a member of `oneof` _ `evaluation_results` .
|
`metricx_result` |
Result for Metricx metric. This field is a member of `oneof` _ `evaluation_results` .
|
`trajectory_exact_match_results` |
Result for trajectory exact match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`trajectory_in_order_match_results` |
Result for trajectory in order match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`trajectory_any_order_match_results` |
Result for trajectory any order match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`trajectory_precision_results` |
Result for trajectory precision metric. This field is a member of `oneof` _ `evaluation_results` .
|
`trajectory_recall_results` |
Results for trajectory recall metric. This field is a member of `oneof` _ `evaluation_results` .
|
`trajectory_single_tool_use_results` |
Results for trajectory single tool use metric. This field is a member of `oneof` _ `evaluation_results` .
|
`rubric_based_instruction_following_result` |
Result for rubric based instruction following metric. This field is a member of `oneof` _ `evaluation_results` .
|

## Methods

### EvaluateInstancesResponse

`EvaluateInstancesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EvaluationService.EvaluateInstances.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesexplanationmetadataoverrideinputsentry_goog_ca77c7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexplanationmetadataoverrideinputsentry_googl_007050.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplanationmetadataoverrideinputsentry_google_f8f39c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadataoverrideinputsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadataOverride.InputsEntry -->

# Class InputsEntry (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatemodelmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitoringJobRequest -->

# Class CreateModelMonitoringJobRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstreamqueryreasoningenginerequest_googlecloud_1a616e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamqueryreasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamQueryReasoningEngineRequest -->

# Class StreamQueryReasoningEngineRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexactmatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringjoblabelsentry_goog_9e8b5d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringjoblabelsentry_googl_815359.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob.LabelsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelopensourcecategory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.OpenSourceCategory -->

# Class OpenSourceCategory (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslogprobsresult_googlecloudaiplatform_v1typesfulfil_01e90c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslogprobsresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LogprobsResult -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfulfillmentinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesevaluation_serviceevaluationserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceClient -->

# Class EvaluationServiceClient (1.134.0)

```
EvaluationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### EvaluationServiceClient

```
EvaluationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the evaluation service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the EvaluationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### evaluate_instances

```
evaluate_instances(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.evaluation_service.EvaluateInstancesRequest,
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
) -> google.cloud.aiplatform_v1.types.evaluation_service.EvaluateInstancesResponse
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
from google.cloud import aiplatform_v1
def sample_evaluate_instances():
# Create a client
client = aiplatform_v1.
```[EvaluationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[EvaluateInstancesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesRequest.html)(
location="location_value",
)
# Make the request
response = client.[evaluate_instances](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceClient.html#google_cloud_aiplatform_v1_services_evaluation_service_EvaluationServiceClient_evaluate_instances)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for EvaluationService.EvaluateInstances. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
`EvaluationServiceClient` |
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
`EvaluationServiceClient` |
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
`EvaluationServiceClient` |
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model -->

# Class Model (1.134.0)

```
Model(
model_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
version: typing.Optional[str] = None,
)
```


Retrieves the model resource and instantiates its representation.

## Parameters |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. A fully-qualified model resource name or model ID. Example: "projects/123/locations/us-central1/models/456" or "456" when project and location are initialized or passed. May optionally contain a version ID or version alias in {model_name}@{version} form. See version arg. |
`project` |
`str`
Optional project to retrieve model from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve model from. If not set, location set in aiplatform.init will be used. |
`version` |
`str`
Optional. Version ID or version alias. When set, the specified model version will be targeted unless overridden in method calls. When not set, the model with the "default" alias will be targeted unless overridden in method calls. No behavior change if only one version of a model exists. |

## Properties

### container_spec

The specification of the container that is to be used when deploying this Model. Not present for AutoML Models.

### create_time

Time this resource was created.

### description

Description of the model.

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

### predict_schemata

The schemata that describe formats of the Model's predictions and explanations, if available.

### preview

Return a Model instance with preview features enabled.

### resource_name

Full qualified resource name, without any version ID.

### supported_deployment_resources_types

List of deployment resource types accepted for this Model.

When this Model is deployed, its prediction resources are described by
the `prediction_resources`

field of the objects returned by
`Endpoint.list_models()`

. Because not all Models support all resource
configuration types, the configuration types this Model supports are
listed here.

If no configuration types are listed, the Model cannot be
deployed to an `Endpoint`

and does not support online predictions
(`Endpoint.predict()`

or `Endpoint.explain()`

). Such a Model can serve
predictions by using a `BatchPredictionJob`

, if it has at least one entry
each in `Model.supported_input_storage_formats`

and
`Model.supported_output_storage_formats`

.

### supported_export_formats

The formats and content types in which this Model may be exported. If empty, this Model is not available for export.

For example, if this model can be exported as a Tensorflow SavedModel and have the artifacts written to Cloud Storage, the expected value would be:

```
{'tf-saved-model': [<ExportableContent.ARTIFACT: 1>]}
```


### supported_input_storage_formats

The formats this Model supports in the `input_config`

field of a
`BatchPredictionJob`

. If `Model.predict_schemata.instance_schema_uri`

exists, the instances should be given as per that schema.

[Read the docs for more on batch prediction formats](https://cloud.google.com/vertex-ai/docs/predictions/batch-predictions#batch_request_input)

If this Model doesn't support any of these formats it means it cannot be
used with a `BatchPredictionJob`

. However, if it has
`supported_deployment_resources_types`

, it could serve online predictions
by using `Endpoint.predict()`

or `Endpoint.explain()`

.

### supported_output_storage_formats

The formats this Model supports in the `output_config`

field of a
`BatchPredictionJob`

.

If both `Model.predict_schemata.instance_schema_uri`

and
`Model.predict_schemata.prediction_schema_uri`

exist, the predictions
are returned together with their instances. In other words, the
prediction has the original instance data first, followed by the actual
prediction content (as per the schema).

[Read the docs for more on batch prediction formats](https://cloud.google.com/vertex-ai/docs/predictions/batch-predictions)

If this Model doesn't support any of these formats it means it cannot be
used with a `BatchPredictionJob`

. However, if it has
`supported_deployment_resources_types`

, it could serve online predictions
by using `Endpoint.predict()`

or `Endpoint.explain()`

.

### training_job

The TrainingJob that uploaded this Model, if any.

Exceptions |
|
|---|---|
Type |
Description |
`api_core.exceptions.NotFound` |
If the Model's training job resource cannot be found on the Vertex service. |

### update_time

Time this resource was last updated.

### uri

Path to the directory containing the Model artifact and any of its supporting files. Not present for AutoML Models.

### version_aliases

User provided version aliases so that a model version can be referenced via
alias (i.e. projects/{project}/locations/{location}/models/{model_id}@{version_alias}
instead of auto-generated version id (i.e.
projects/{project}/locations/{location}/models/{model_id}@{version_id}).
The format is `a-z][a-zA-Z0-9-]`

{0,126}[a-z0-9] to distinguish from
version_id. A default version alias will be created for the first version
of the model, and there must be exactly one default version alias for a model.

### version_create_time

Timestamp when this version was created.

### version_description

The description of this version.

### version_id

The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation.

### version_update_time

Timestamp when this version was updated.

### versioned_resource_name

The fully-qualified resource name, including the version ID. For example, projects/{project}/locations/{location}/models/{model_id}@{version_id}

### versioning_registry

The registry of model versions associated with this Model instance.

## Methods

### batch_predict

```
batch_predict(
job_display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bigquery_source: typing.Optional[str] = None,
instances_format: str = "jsonl",
gcs_destination_prefix: typing.Optional[str] = None,
bigquery_destination_prefix: typing.Optional[str] = None,
predictions_format: str = "jsonl",
model_parameters: typing.Optional[typing.Dict] = None,
machine_type: typing.Optional[str] = None,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
starting_replica_count: typing.Optional[int] = None,
max_replica_count: typing.Optional[int] = None,
generate_explanation: typing.Optional[bool] = False,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
batch_size: typing.Optional[int] = None,
service_account: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.BatchPredictionJob
```


Creates a batch prediction job using this Model and outputs
prediction results to the provided destination prefix in the specified
`predictions_format`

. One source and one destination prefix are
required.

Example usage: my_model.batch_predict( job_display_name="prediction-123", gcs_source="gs://example-bucket/instances.csv", instances_format="csv", bigquery_destination_prefix="projectId.bqDatasetId.bqTableId" )

Parameters |
|
|---|---|
Name |
Description |
`job_display_name` |
`str`
Optional. The user-defined name of the BatchPredictionJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`gcs_source` |
`typing.Union[str, typing.Sequence[str], NoneType]`
Optional[Sequence[str]] = None Google Cloud Storage URI(-s) to your instances to run batch prediction on. They must match |
`bigquery_source` |
`typing.Optional[str]`
Optional[str] = None BigQuery URI to a table, up to 2000 characters long. For example: |
`instances_format` |
`str`
str = "jsonl" The format in which instances are provided. Must be one of the formats listed in |
`gcs_destination_prefix` |
`typing.Optional[str]`
Optional[str] = None The Google Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is |
`bigquery_destination_prefix` |
`typing.Optional[str]`
Optional[str] = None The BigQuery URI to a project or table, up to 2000 characters long. When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist. Accepted forms: |
`predictions_format` |
`str`
str = "jsonl" Required. The format in which Vertex AI outputs the predictions, must be one of the formats specified in |
`model_parameters` |
`typing.Optional[typing.Dict]`
Optional[Dict] = None Optional. The parameters that govern the predictions. The schema of the parameters may be specified via the Model's |
`machine_type` |
`typing.Optional[str]`
Optional[str] = None Optional. The type of machine for running batch prediction on dedicated resources. Not specifying machine type will result in batch prediction job being run with automatic resources. |
`accelerator_type` |
`typing.Optional[str]`
Optional[str] = None Optional. The type of accelerator(s) that may be attached to the machine as per |
`accelerator_count` |
`typing.Optional[int]`
Optional[int] = None Optional. The number of accelerators to attach to the |
`starting_replica_count` |
`typing.Optional[int]`
Optional[int] = None The number of machine replicas used at the start of the batch operation. If not set, Vertex AI decides starting number, not greater than |
`max_replica_count` |
`typing.Optional[int]`
Optional[int] = None The maximum number of machine replicas the batch operation may be scaled to. Only used if |
`generate_explanation` |
`bool`
Optional. Generate explanation along with the batch prediction results. This will cause the batch prediction output to include explanations based on the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Explanation metadata configuration for this BatchPredictionJob. Can be specified only if |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. Can be specified only if |
`labels` |
`typing.Optional[typing.Dict[str, str]]`
Optional[Dict[str, str]] = None Optional. The labels with user-defined metadata to organize your BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`typing.Optional[google.auth.credentials.Credentials]`
Optional[auth_credentials.Credentials] = None Optional. Custom credentials to use to create this batch prediction job. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`batch_size` |
`int`
Optional. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |

Returns |
|
|---|---|
Type |
Description |
`job (jobs.BatchPredictionJob)` |
Instantiated representation of the created batch prediction job. |

### copy

```
copy(
destination_location: str,
destination_model_id: typing.Optional[str] = None,
destination_parent_model: typing.Optional[str] = None,
encryption_spec_key_name: typing.Optional[str] = None,
copy_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Copys a model and returns a Model representing the copied Model resource. This method is a blocking call.

Example usage: copied_model = my_model.copy( destination_location="us-central1" )

Parameters |
|
|---|---|
Name |
Description |
`destination_location` |
`str`
The destination location to copy the model to. |
`destination_model_id` |
`str`
Optional. The ID to use for the copied Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`destination_parent_model` |
`str`
Optional. The resource name or model ID of an existing model that the newly-copied model will be a version of. Only set this field when copying as a new version of an existing model. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`copy_request_timeout` |
`float`
Optional. The timeout for the copy request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both `destination_model_id` and `destination_parent_model` are set. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the copied model resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### deploy

```
deploy(
endpoint: typing.Optional[
typing.Union[
google.cloud.aiplatform.models.Endpoint,
google.cloud.aiplatform.models.PrivateEndpoint,
]
] = None,
deployed_model_display_name: typing.Optional[str] = None,
traffic_percentage: typing.Optional[int] = 0,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
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
encryption_spec_key_name: typing.Optional[str] = None,
network: typing.Optional[str] = None,
sync=True,
deploy_request_timeout: typing.Optional[float] = None,
autoscaling_target_cpu_utilization: typing.Optional[int] = None,
autoscaling_target_accelerator_duty_cycle: typing.Optional[int] = None,
autoscaling_target_request_count_per_minute: typing.Optional[int] = None,
autoscaling_target_pubsub_num_undelivered_messages: typing.Optional[int] = None,
autoscaling_pubsub_subscription_labels: typing.Optional[
typing.Dict[str, str]
] = None,
enable_access_logging=False,
disable_container_logging: bool = False,
private_service_connect_config: typing.Optional[
google.cloud.aiplatform.models.PrivateEndpoint.PrivateServiceConnectConfig
] = None,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform.models.DeploymentResourcePool
] = None,
reservation_affinity_type: typing.Optional[str] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
spot: bool = False,
fast_tryout_enabled: bool = False,
system_labels: typing.Optional[typing.Dict[str, str]] = None,
required_replica_count: typing.Optional[int] = 0,
) -> typing.Union[
google.cloud.aiplatform.models.Endpoint,
google.cloud.aiplatform.models.PrivateEndpoint,
]
```


Deploys model to endpoint. Endpoint will be created if unspecified.

Parameters |
|
|---|---|
Name |
Description |
`endpoint` |
`Union[Endpoint, PrivateEndpoint]`
Optional. Public or private Endpoint to deploy model to. If not specified, endpoint display name will be model display name+'_endpoint'. |
`deployed_model_display_name` |
`str`
Optional. The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`traffic_percentage` |
`int`
Optional. Desired traffic to newly deployed model. Defaults to 0 if there are pre-existing deployed models. Defaults to 100 if there are no pre-existing deployed models. Negative values should not be provided. Traffic of previously deployed models at the endpoint will be scaled down to accommodate new deployed model's traffic. Should not be provided if traffic_split is provided. |
`traffic_split` |
`Dict[str, int]`
Optional. A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. Key for model being deployed is "0". Should not be provided if traffic_percentage is provided. |
`machine_type` |
`str`
Optional. The type of machine. Not specifying machine type will result in model to be deployed with automatic resources. |
`min_replica_count` |
`int`
Optional. The minimum number of machine replicas this deployed model will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the smaller value of min_replica_count or 1 will be used. |
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
Optional. The TPU topology to use for the DeployedModel. Requireid for CloudTPU multihost deployments. |
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
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the Endpoint, if created, will be peered to. E.g. "projects/12345/global/networks/myVPC" Private services access must already be configured for the network. If set or aiplatform.init(network=...) has been set, a PrivateEndpoint will be created. If left unspecified, an Endpoint will be created. Read more about PrivateEndpoints |
`deploy_request_timeout` |
`float`
Optional. The timeout for the deploy request in seconds. |
`autoscaling_target_cpu_utilization` |
`int`
Target CPU Utilization to use for Autoscaling Replicas. A default value of 60 will be used if not specified. |
`autoscaling_target_accelerator_duty_cycle` |
`int`
Target Accelerator Duty Cycle. Must also set accelerator_type and accelerator_count if specified. A default value of 60 will be used if not specified. |
`autoscaling_target_request_count_per_minute` |
`int`
Optional. The target number of requests per minute for autoscaling. If set, the model will be scaled based on the number of requests it receives. |
`autoscaling_target_pubsub_num_undelivered_messages` |
`int`
Optional. The target number of pubsub undelivered messages for autoscaling. If set, the model will be scaled based on the pubsub queue size. |
`autoscaling_pubsub_subscription_labels` |
`Dict[str, str]`
Optional. Monitored resource labels as key value pairs for metric filtering for pubsub_num_undelivered_messages. |
`disable_container_logging` |
`bool`
If True, container logs from the deployed model will not be written to Cloud Logging. Defaults to False. |
`private_service_connect_config` |
`PrivateEndpoint.PrivateServiceConnectConfig`
If true, the endpoint can be accessible via |
`deployment_resource_pool` |
`DeploymentResourcePool`
Resource pool where the model will be deployed. All models that are deployed to the same DeploymentResourcePool will be hosted in a shared model server. If provided, will override replica count arguments. |
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
`fast_tryout_enabled` |
`bool`
Optional. Defaults to False. If True, model will be deployed using faster deployment path. Useful for quick experiments. Not for production workloads. Only available for most popular models with certain machine types. |
`system_labels` |
`Dict[str, str]`
Optional. System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`required_replica_count` |
`int`
Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial model deployment/mutation is desired, with a value greater than or equal to 1 and fewer than or equal to min_replica_count. If set, the model deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_access_logging` |
`bool`
Whether to enable endpoint access logging. Defaults to False. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `traffic_split` is set for PrivateEndpoint. |

Returns |
|
|---|---|
Type |
Description |
`endpoint (Union[Endpoint, PrivateEndpoint])` |
Endpoint with the deployed model. |

### evaluate

```
evaluate(
prediction_type: str,
target_field_name: str,
gcs_source_uris: typing.Optional[typing.List[str]] = None,
bigquery_source_uri: typing.Optional[str] = None,
bigquery_destination_output_uri: typing.Optional[str] = None,
class_labels: typing.Optional[typing.List[str]] = None,
prediction_label_column: typing.Optional[str] = None,
prediction_score_column: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
generate_feature_attributions: bool = False,
evaluation_pipeline_display_name: typing.Optional[str] = None,
evaluation_metrics_display_name: typing.Optional[str] = None,
network: typing.Optional[str] = None,
encryption_spec_key_name: typing.Optional[str] = None,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
enable_caching: typing.Optional[bool] = None,
) -> google.cloud.aiplatform.model_evaluation.model_evaluation_job._ModelEvaluationJob
```


Creates a model evaluation job running on Vertex Pipelines and returns the resulting ModelEvaluationJob resource.

Example usage:

```
```
my_model = Model(
model_name="projects/123/locations/us-central1/models/456"
)
my_evaluation_job = my_model.evaluate(
prediction_type="classification",
target_field_name="type",
data_source_uris=["gs://sdk-model-eval/my-prediction-data.csv"],
staging_bucket="gs://my-staging-bucket/eval_pipeline_root",
)
my_evaluation_job.wait()
my_evaluation = my_evaluation_job.get_model_evaluation()
my_evaluation.metrics
```
```


Parameters |
|
|---|---|
Name |
Description |
`prediction_type` |
`str`
Required. The problem type being addressed by this evaluation run. 'classification' and 'regression' are the currently supported problem types. |
`target_field_name` |
`str`
Required. The column name of the field containing the label for this prediction task. |
`gcs_source_uris` |
`List[str]`
Optional. A list of Cloud Storage data files containing the ground truth data to use for this evaluation job. These files should contain your model's prediction column. Currently only Google Cloud Storage urls are supported, for example: "gs://path/to/your/data.csv". The provided data files must be either CSV or JSONL. One of |
`bigquery_source_uri` |
`str`
Optional. A bigquery table URI containing the ground truth data to use for this evaluation job. This uri should be in the format 'bq://my-project-id.dataset.table'. One of |
`bigquery_destination_output_uri` |
`str`
Optional. A bigquery table URI where the Batch Prediction job associated with your Model Evaluation will write prediction output. This can be a BigQuery URI to a project ('bq://my-project'), a dataset ('bq://my-project.my-dataset'), or a table ('bq://my-project.my-dataset.my-table'). Required if |
`class_labels` |
`List[str]`
Optional. For custom (non-AutoML) classification models, a list of possible class names, in the same order that predictions are generated. This argument is required when prediction_type is 'classification'. For example, in a classification model with 3 possible classes that are outputted in the format: [0.97, 0.02, 0.01] with the class names "cat", "dog", and "fish", the value of |
`prediction_label_column` |
`str`
Optional. The column name of the field containing classes the model is scoring. Formatted to be able to find nested columns, delimited by |
`prediction_score_column` |
`str`
Optional. The column name of the field containing batch prediction scores. Formatted to be able to find nested columns, delimited by |
`staging_bucket` |
`str`
Optional. The GCS directory to use for staging files from this evaluation job. Defaults to the value set in aiplatform.init(staging_bucket=...) if not provided. Required if staging_bucket is not set in aiplatform.init(). |
`service_account` |
`str`
Specifies the service account for workload run-as account for this Model Evaluation PipelineJob. Users submitting jobs must have act-as permission on this run-as account. The service account running this Model Evaluation job needs the following permissions: Dataflow Worker, Storage Admin, Vertex AI Administrator, and Vertex AI Service Agent. |
`generate_feature_attributions` |
`boolean`
Optional. Whether the model evaluation job should generate feature attributions. Defaults to False if not specified. |
`evaluation_pipeline_display_name` |
`str`
Optional. The display name of your model evaluation job. This is the display name that will be applied to the Vertex Pipeline run for your evaluation job. If not set, a display name will be generated automatically. |
`evaluation_metrics_display_name` |
`str`
Optional. The display name of the model evaluation resource uploaded to Vertex from your Model Evaluation pipeline. |
`network` |
`str`
The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the job is not peered with any network. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`experiment` |
`Union[str, experiments_resource.Experiment]`
Optional. The Vertex AI experiment name or instance to associate to the PipelineJob executing this model evaluation job. Metrics produced by the PipelineJob as system.Metric Artifacts will be associated as metrics to the provided experiment, and parameters from this PipelineJob will be associated as parameters to the provided experiment. |
`enable_caching` |
`bool`
Optional. Whether to turn on caching for the run. If this is not set, defaults to the compile time settings, which are True for all tasks by default, while users may specify different caching options for individual tasks. If this is set, the setting applies to all tasks in the pipeline. Overrides the compile time settings. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If staging_bucket was not set in aiplatform.init() and staging_bucket was not provided. If the provided `prediction_type` is not valid. If the provided `data_source_uris` don't start with 'gs://'. |

Returns |
|
|---|---|
Type |
Description |
`model_evaluation.ModelEvaluationJob` |
Instantiated representation of the _ModelEvaluationJob. |

### export_model

```
export_model(
export_format_id: str,
artifact_destination: typing.Optional[str] = None,
image_destination: typing.Optional[str] = None,
sync: bool = True,
) -> typing.Dict[str, str]
```


Exports a trained, exportable Model to a location specified by the user.
A Model is considered to be exportable if it has at least one `supported_export_formats`

.
Either `artifact_destination`

or `image_destination`

must be provided.

Example Usage: my_model.export( export_format_id="tf-saved-model", artifact_destination="gs://my-bucket/models/" )

```
or
my_model.export(
export_format_id="custom-model",
image_destination="us-central1-docker.pkg.dev/projectId/repo/image"
)
```


Parameters |
|
|---|---|
Name |
Description |
`export_format_id` |
`str`
Required. The ID of the format in which the Model must be exported. The list of export formats that this Model supports can be found by calling |
`artifact_destination` |
`str`
The Cloud Storage location where the Model artifact is to be written to. Under the directory given as the destination a new one with name " |
`image_destination` |
`str`
The Google Container Registry or Artifact Registry URI where the Model container image will be copied to. Accepted forms: - Google Container Registry path. For example: |
`sync` |
`bool`
Whether to execute this export synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If model does not support exporting. |
`ValueError` |
If invalid arguments or export formats are provided. |

Returns |
|
|---|---|
Type |
Description |
`output_info (Dict[str, str])` |
Details of the completed export with output destination paths to the artifacts or container image. |

### get_model_evaluation

```
get_model_evaluation(
evaluation_id: typing.Optional[str] = None,
) -> typing.Optional[
google.cloud.aiplatform.model_evaluation.model_evaluation.ModelEvaluation
]
```


Returns a ModelEvaluation resource and instantiates its representation. If no evaluation_id is passed, it will return the first evaluation associated with this model. If the aiplatform.Model resource was instantiated with a version, this will return a Model Evaluation from that version. If no version was specified when instantiating the Model resource, this will return an Evaluation from the default version.

Example usage: my_model = Model( model_name="projects/123/locations/us-central1/models/456" )

```
my_evaluation = my_model.get_model_evaluation(
evaluation_id="789"
)
# If no arguments are passed, this method returns the first evaluation for the model
my_evaluation = my_model.get_model_evaluation()
```


Parameter |
|
|---|---|
Name |
Description |
`evaluation_id` |
`str`
Optional. The ID of the model evaluation to retrieve. |

Returns |
|
|---|---|
Type |
Description |
`model_evaluation.ModelEvaluation` |
Instantiated representation of the ModelEvaluation resource. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.models.Model]
```


List all Model resource instances.

Example Usage: aiplatform.Model.list( filter='labels.my_label="my_label_value" AND display_name="my_model"', )

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
`List[models.Model]` |
A list of Model resource objects |

### list_model_evaluations

```
list_model_evaluations() -> (
typing.List[
google.cloud.aiplatform.model_evaluation.model_evaluation.ModelEvaluation
]
)
```


List all Model Evaluation resources associated with this model. If this Model resource was instantiated with a version, the Model Evaluation resources for that version will be returned. If no version was provided when the Model resource was instantiated, Model Evaluation resources will be returned for the default version.

Example Usage: my_model = Model( model_name="projects/123/locations/us-central1/models/456@1" )

```
my_evaluations = my_model.list_model_evaluations()
```


Returns |
|
|---|---|
Type |
Description |
`List[model_evaluation.ModelEvaluation]` |
List of ModelEvaluation resources for the model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
) -> google.cloud.aiplatform.models.Model
```


Updates a model.

Example usage: my_model = my_model.update( display_name="my-model", description="my description", labels={'key': 'value'}, )

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
The description of the model. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `labels` is not the correct format. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Updated model resource. |

### upload

```
upload(
serving_container_image_uri: typing.Optional[str] = None,
*,
artifact_uri: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: bool = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
serving_container_predict_route: typing.Optional[str] = None,
serving_container_health_route: typing.Optional[str] = None,
serving_container_invoke_route_prefix: typing.Optional[str] = None,
description: typing.Optional[str] = None,
serving_container_command: typing.Optional[typing.Sequence[str]] = None,
serving_container_args: typing.Optional[typing.Sequence[str]] = None,
serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
serving_container_grpc_ports: typing.Optional[typing.Sequence[int]] = None,
local_model: typing.Optional[LocalModel] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
display_name: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[float] = None,
serving_container_deployment_timeout: typing.Optional[int] = None,
serving_container_shared_memory_size_mb: typing.Optional[int] = None,
serving_container_startup_probe_exec: typing.Optional[typing.Sequence[str]] = None,
serving_container_startup_probe_period_seconds: typing.Optional[int] = None,
serving_container_startup_probe_timeout_seconds: typing.Optional[int] = None,
serving_container_health_probe_exec: typing.Optional[typing.Sequence[str]] = None,
serving_container_health_probe_period_seconds: typing.Optional[int] = None,
serving_container_health_probe_timeout_seconds: typing.Optional[int] = None,
model_garden_source_model_name: typing.Optional[str] = None,
model_garden_source_model_version_id: typing.Optional[str] = None
) -> Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload( display_name="my-model", artifact_uri="gs://my-model/saved-model", serving_container_image_uri="tensorflow/serving" )

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If explanation_metadata is specified while explanation_parameters is not. Also if model directory does not contain a supported model file. If `local_model` is specified but `serving_container_spec.image_uri` in the `local_model` is None. If `local_model` is not specified and `serving_container_image_uri` is None. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### upload_scikit_learn_model_file

```
upload_scikit_learn_model_file(
model_file_path: str,
sklearn_version: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload_scikit_learn_model_file( model_file_path="iris.sklearn_model.joblib" )

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If explanation_metadata is specified while explanation_parameters is not. Also if model directory does not contain a supported model file. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### upload_tensorflow_saved_model

```
upload_tensorflow_saved_model(
saved_model_dir: str,
tensorflow_version: typing.Optional[str] = None,
use_gpu: bool = False,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[str] = None,
) -> google.cloud.aiplatform.models.Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload_scikit_learn_model_file( model_file_path="iris.tensorflow_model.SavedModel" )

Parameters |
|
|---|---|
Name |
Description |
`upload_request_timeout` |
`float`
Optional. The timeout for the upload request in seconds. |
`saved_model_dir` |
`str`
Required. Local directory of the Tensorflow SavedModel. |
`tensorflow_version` |
`str`
Optional. The version of the Tensorflow serving container. Supported versions: ["0.15", "2.1", "2.2", "2.3", "2.4", "2.5", "2.6", "2.7"]. If the version is not specified, the latest version is used. |
`use_gpu` |
`bool`
Whether to use GPU for model serving. |
`display_name` |
`str`
Optional. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
The description of the model. |
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model that the newly-uploaded model will be a version of. Only set this field when uploading a new version of an existing model. |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of this model without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the newly-uploaded model version will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that a model version can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`version_description` |
`str`
Optional. The description of the model version being uploaded. |
`instance_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in |
`parameters_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via |
`prediction_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`staging_bucket` |
`str`
Optional. Bucket to stage local model artifacts. Overrides staging_bucket set in aiplatform.init. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If explanation_metadata is specified while explanation_parameters is not. Also if model directory does not contain a supported model file. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### upload_xgboost_model_file

```
upload_xgboost_model_file(
model_file_path: str,
xgboost_version: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload_xgboost_model_file( model_file_path="iris.xgboost_model.bst" )

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If model directory does not contain a supported model file. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: __prediction_v1beta1___googlecloudaiplatform_v1typesmodelcontainerspec___googlec_757ab0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _prediction_v1beta1___googlecloudaiplatform_v1typesmodelcontainerspec___googlecl_2cb16e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: prediction_v1beta1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/prediction_v1beta1 -->

# Types for Google Cloud Aiplatform V1beta1 Schema Predict Prediction v1beta1 API

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageObjectDetectionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageSegmentationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularRegressionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextExtractionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextSentimentPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Text Sentiment

#### sentiment()

The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive).

**Type**

#### sentiment(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TimeSeriesForecastingPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Time Series Forecasting.

#### value()

The regression value.

**Type**

#### value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoActionRecognitionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

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

[google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame](https://docs.cloud.google.com/python/docs/reference/aiplatform/prediction_v1beta1/types_.md#google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame)]

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

#### frames(*: MutableSequence[[Frame](../prediction_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame)_ )

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelcontainerspec___googlecloudaiplatform_v1type_b4d20b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelcontainerspec___googlecloudaiplatform_v1types_0411d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelcontainerspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelContainerSpec -->

# Class ModelContainerSpec (1.134.0)

`ModelContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a container for serving predictions. Some fields in
this message correspond to fields in the ```
Kubernetes Container v1
core
specification <https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core>
```

__.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. Immutable. URI of the Docker image to be used as the custom container for serving predictions. This URI must identify an image in Artifact Registry or Container Registry. Learn more about the `container publishing requirements |
`command` |
`MutableSequence[str]`
Immutable. Specifies the command that runs when the container starts. This overrides the container's `ENTRYPOINT ` __.
Specify this field as an array of executable and arguments,
similar to a Docker `ENTRYPOINT` 's "exec" form, not its
"shell" form.
If you do not specify this field, then the container's
`ENTRYPOINT` runs, in conjunction with the
args
field or the container's
```CMD` ` ` __,
if either exists. If this field is not specified and the
container does not have an `ENTRYPOINT` , then refer to the
Docker documentation about `how ` CMD` and ` ENTRYPOINT`
interact |
`args` |
`MutableSequence[str]`
Immutable. Specifies arguments for the command that runs when the container starts. This overrides the container's CMD` ` ` __
and `CMD` determine what runs based on their default
behavior. See the Docker documentation about `how ` CMD`
and `ENTRYPOINT`
interact |
`env` |
`MutableSequence[`
Immutable. List of environment variables to set in the container. After the container starts running, code running in the container can read these environment variables. Additionally, the command and args fields can reference these variables. Later entries in this list can also reference earlier entries. For example, the following example sets the variable `VAR_2` to have the
value `foo bar` :
.. code:: json
[
{
"name": "VAR_1",
"value": "foo"
},
{
"name": "VAR_2",
"value": "$(VAR_1) bar"
}
]
If you switch the order of the variables in the example,
then the expansion does not occur.
This field corresponds to the `env` field of the
Kubernetes Containers `v1 core
API |
`ports` |
`MutableSequence[`
Immutable. List of ports to expose from the container. Vertex AI sends any prediction requests that it receives to the first port on this list. Vertex AI also sends `liveness and health checks |
`predict_route` |
`str`
Immutable. HTTP path on the container to send prediction requests to. Vertex AI forwards requests sent using projects.locations.endpoints.predict to this path on the container's IP address and port. Vertex AI then returns the container's response in the API response. For example, if you set this field to `/foo` , then when
Vertex AI receives a prediction request, it forwards the
request body in a POST request to the `/foo` path on the
port of your container specified by the first value of this
`ModelContainerSpec` 's
ports
field.
If you don't specify this field, it defaults to the
following value when you [deploy this Model to an
Endpoint][google.cloud.aiplatform.v1.EndpointService.DeployModel]:
/v1/endpoints/ENDPOINT/deployedModels/DEPLOYED_MODEL:predict
The placeholders in this value are replaced as follows:
- ENDPOINT: The last segment (following `endpoints/` )of
the Endpoint.name][] field of the Endpoint where this
Model has been deployed. (Vertex AI makes this value
available to your container code as the
AIP_ENDPOINT_ID`` environment variable |
`health_route` |
`str`
Immutable. HTTP path on the container to send health checks to. Vertex AI intermittently sends GET requests to this path on the container's IP address and port to check that the container is healthy. Read more about `health checks |
`invoke_route_prefix` |
`str`
Immutable. Invoke route prefix for the custom container. "/\*" is the only supported value right now. By setting this field, any non-root route on this model will be accessible with invoke http call eg: "/invoke/foo/bar", however the [PredictionService.Invoke] RPC is not supported yet. Only one of `predict_route` or `invoke_route_prefix` can
be set, and we default to using `predict_route` if this
field is not set. If this field is set, the Model can only
be deployed to dedicated endpoint.
|
`grpc_ports` |
`MutableSequence[`
Immutable. List of ports to expose from the container. Vertex AI sends gRPC prediction requests that it receives to the first port on this list. Vertex AI also sends liveness and health checks to this port. If you do not specify this field, gRPC requests to the container will be disabled. Vertex AI does not use ports other than the first one listed. This field corresponds to the `ports` field of the
Kubernetes Containers v1 core API.
|
`deployment_timeout` |
`google.protobuf.duration_pb2.Duration`
Immutable. Deployment timeout. Limit for deployment timeout is 2 hours. |
`shared_memory_size_mb` |
`int`
Immutable. The amount of the VM memory to reserve as the shared memory for the model in megabytes. |
`startup_probe` |
Immutable. Specification for Kubernetes startup probe. |
`health_probe` |
Immutable. Specification for Kubernetes readiness probe. |
`liveness_probe` |
Immutable. Specification for Kubernetes liveness probe. |

## Methods

### ModelContainerSpec

`ModelContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a container for serving predictions. Some fields in
this message correspond to fields in the ```
Kubernetes Container v1
core
specification <https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core>
```

__.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelevaluationslicesliceslicespecconfigsentry_go_6a462a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelevaluationslicesliceslicespecconfigsentry_goo_a1c86a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelevaluationslicesliceslicespecconfigsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.ConfigsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturemonitoringstatsanomaly.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Feature.MonitoringStatsAnomaly -->

# Class MonitoringStatsAnomaly (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescompletetrialrequest_googlecloudaiplatform_v1_57ad74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescompletetrialrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CompleteTrialRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatedeploymentresourcepoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolRequest -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesendpointtrafficsplitentry_googlecloudaiplat_6c41d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesendpointtrafficsplitentry_googlecloudaiplatf_3fa25b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesendpointtrafficsplitentry_googlecloudaiplatfo_736f38.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesendpointtrafficsplitentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.TrafficSplitEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkeymatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchMetricValue -->

# Class ToolParameterKeyMatchMetricValue (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeploymodelrequesttrafficsplitentry_googlecloudaip_1353cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeploymodelrequesttrafficsplitentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.TrafficSplitEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistmetadatastoresrequest_googlecloudaiplatform_v_09e214.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmetadatastoresrequest_googlecloudaiplatform_v1_307e41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmetadatastoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesoutputinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputInfo -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_monitoring_service_googlecloudaiplat_687dae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescustomjobwebaccessurisentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob.WebAccessUrisEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesexample_store_serviceexamplestoreserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient -->

# Class ExampleStoreServiceAsyncClient (1.134.0)

```
ExampleStoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing and retrieving few-shot examples.

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
`ExampleStoreServiceTransport` |
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

### ExampleStoreServiceAsyncClient

```
ExampleStoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the example store service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ExampleStoreServiceTransport,Callable[..., ExampleStoreServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ExampleStoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_example_store

```
create_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.CreateExampleStoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
example_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.example_store.ExampleStore
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


Create an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
example_store = aiplatform_v1beta1.[ExampleStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore.html)()
example_store.display_name = "display_name_value"
example_store.example_store_config.vertex_embedding_model = "vertex_embedding_model_value"
request = aiplatform_v1beta1.[CreateExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExampleStoreRequest.html)(
parent="parent_value",
example_store=example_store,
)
# Make the request
operation = client.[create_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_create_example_store)(request=request)
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
The request object. Request message for ExampleStoreService.CreateExampleStore. |
`parent` |
Required. The resource name of the Location to create the ExampleStore in. Format: |
`example_store` |
Required. The Example Store to be created. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_example_store

```
delete_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.DeleteExampleStoreRequest,
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


Delete an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExampleStoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_delete_example_store)(request=request)
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
The request object. Request message for ExampleStoreService.DeleteExampleStore. |
`name` |
Required. The resource name of the ExampleStore to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### example_store_path

`example_store_path(project: str, location: str, example_store: str) -> str`


Returns a fully-qualified example_store string.

### fetch_examples

```
fetch_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
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
google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesAsyncPager
)
```


Get Examples from the Example Store.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_fetch_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesRequest.html)(
example_store="example_store_value",
)
# Make the request
page_result = client.[fetch_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_fetch_examples)(request=request)
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
The request object. Request message for ExampleStoreService.FetchExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.FetchExamples. Iterating over this object will yield results and resolve additional pages automatically. |

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
`ExampleStoreServiceAsyncClient` |
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
`ExampleStoreServiceAsyncClient` |
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
`ExampleStoreServiceAsyncClient` |
The constructed client. |

### get_example_store

```
get_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.GetExampleStoreRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.example_store.ExampleStore
```


Get an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExampleStoreRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_get_example_store)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.GetExampleStore. |
`name` |
Required. The resource name of the ExampleStore. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents an executable service to manage and retrieve examples. |

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
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport
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

### list_example_stores

```
list_example_stores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
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
google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresAsyncPager
)
```


List ExampleStores in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_example_stores():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListExampleStoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_example_stores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_list_example_stores)(request=request)
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
The request object. Request message for ExampleStoreService.ListExampleStores. |
`parent` |
Required. The resource name of the Location to list the ExampleStores from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.ListExampleStores. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_example_store_path

`parse_example_store_path(path: str) -> typing.Dict[str, str]`


Parses a example_store path into its component segments.

### remove_examples

```
remove_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.RemoveExamplesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.example_store_service.RemoveExamplesResponse
```


Remove Examples from the Example Store.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_remove_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RemoveExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesRequest.html)(
example_store="example_store_value",
)
# Make the request
response = await client.[remove_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_remove_examples)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.RemoveExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.RemoveExamples. |

### search_examples

```
search_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.SearchExamplesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.example_store_service.SearchExamplesResponse
```


Search for similar Examples for given selection criteria.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_search_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
stored_contents_example_parameters = aiplatform_v1beta1.[StoredContentsExampleParameters](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleParameters.html)()
stored_contents_example_parameters.search_key = "search_key_value"
request = aiplatform_v1beta1.[SearchExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesRequest.html)(
stored_contents_example_parameters=stored_contents_example_parameters,
example_store="example_store_value",
)
# Make the request
response = await client.[search_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_search_examples)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.SearchExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.SearchExamples. |

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

### update_example_store

```
update_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.UpdateExampleStoreRequest,
dict,
]
] = None,
*,
example_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.example_store.ExampleStore
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


Update an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
example_store = aiplatform_v1beta1.[ExampleStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore.html)()
example_store.display_name = "display_name_value"
example_store.example_store_config.vertex_embedding_model = "vertex_embedding_model_value"
request = aiplatform_v1beta1.[UpdateExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreRequest.html)(
example_store=example_store,
)
# Make the request
operation = client.[update_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_update_example_store)(request=request)
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
The request object. Request message for ExampleStoreService.UpdateExampleStore. |
`example_store` |
Required. The Example Store which replaces the resource on the server. This corresponds to the |
`update_mask` |
Optional. Mask specifying which fields to update. Supported fields: :: * |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### upsert_examples

```
upsert_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.UpsertExamplesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.example_store_service.UpsertExamplesResponse
```


Create or update Examples in the Example Store.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upsert_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
examples = aiplatform_v1beta1.[Example](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Example.html)()
examples.stored_contents_example.contents_example.contents.parts.text = "text_value"
examples.stored_contents_example.contents_example.expected_contents.content.parts.text = "text_value"
request = aiplatform_v1beta1.[UpsertExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesRequest.html)(
example_store="example_store_value",
examples=examples,
)
# Make the request
response = await client.[upsert_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_upsert_examples)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.UpsertExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.UpsertExamples. |

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
