---
source_url: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient
fetched_at: 2026-02-01T07:49:35.455206
---

# Class JobsClient (0.15.0)

```
JobsClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.jobs.transports.base.JobsTransport,
typing.Callable[
[...], google.cloud.run_v2.services.jobs.transports.base.JobsTransport
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Cloud Run Job Control Plane API.

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
`JobsTransport` |
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

### JobsClient

```
JobsClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.run_v2.services.jobs.transports.base.JobsTransport,
typing.Callable[
[...], google.cloud.run_v2.services.jobs.transports.base.JobsTransport
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the jobs client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,JobsTransport,Callable[..., JobsTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the JobsTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_job

```
create_job(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.job.CreateJobRequest, dict]
] = None,
*,
parent: typing.Optional[str] = None,
job: typing.Optional[google.cloud.run_v2.types.job.Job] = None,
job_id: typing.Optional[str] = None,
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


Creates a Job.

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
def sample_create_job():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
job = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[Job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job.html)()
job.start_execution_token = "start_execution_token_value"
job.template.template.max_retries = 1187
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[CreateJobRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateJobRequest.html)(
parent="parent_value",
job=job,
job_id="job_id_value",
)
# Make the request
operation = client.[create_job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_create_job)(request=request)
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
The request object. Request message for creating a Job. |
`parent` |
`str`
Required. The location and project in which this Job should be created. Format: projects/{project}/locations/{location}, where {project} can be project id or number. This corresponds to the |
`job` |
Required. The Job instance to create. This corresponds to the |
`job_id` |
`str`
Required. The unique identifier for the Job. The name of the job becomes {parent}/jobs/{job_id}. This corresponds to the |
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

### crypto_key_path

`crypto_key_path(project: str, location: str, key_ring: str, crypto_key: str) -> str`


Returns a fully-qualified crypto_key string.

### delete_job

```
delete_job(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.job.DeleteJobRequest, dict]
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


Deletes a Job.

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
def sample_delete_job():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[DeleteJobRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_delete_job)(request=request)
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
The request object. Request message to delete a Job by its full name. |
`name` |
`str`
Required. The full name of the Job. Format: projects/{project}/locations/{location}/jobs/{job}, where {project} can be project id or number. This corresponds to the |
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
`JobsClient` |
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
`JobsClient` |
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
`JobsClient` |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM Access Control policy currently in effect for the given Job. This result does not include any inherited policies.

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
def sample_get_iam_policy():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = iam_policy_pb2.GetIamPolicyRequest(
resource="resource_value",
)
# Make the request
response = client.[get_iam_policy](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_get_iam_policy)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
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
`google.iam.v1.policy_pb2.Policy` |
An Identity and Access Management (IAM) policy, which specifies access controls for Google Cloud resources. A Policy is a collection of bindings. A binding binds one or more members, or principals, to a single role. Principals can be user accounts, service accounts, Google groups, and domains (such as G Suite). A role is a named list of permissions; each role can be an IAM predefined role or a user-created custom role. For some types of Google Cloud resources, a binding can also specify a condition, which is a logical expression that allows access to a resource only if the expression evaluates to true. A condition can add constraints based on attributes of the request, the resource, or both. To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies). **JSON example:** :literal:` { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": [ "user:eve@example.com" ], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ],="" "etag":="" "bwwwja0yfja=", " version":="" 3="">` \ \` **YAML example:** :literal:` bindings: - members: - user:mike@example.com - group:admins@example.com - domain:google.com - serviceAccount:my-project-id@appspot.gserviceaccount.com role: roles/resourcemanager.organizationAdmin - members: - user:eve@example.com role: roles/resourcemanager.organizationViewer condition: title: expirable access description: Does not grant access after Sep 2020 expression: request.time < timestamp('2020-10-01t00:00:00.000z')="" etag:="" bwwwja0yfja="version:">`\ \` For a description of IAM and its features, see the [IAM documentation](https://cloud.google.com/iam/docs/). |

### get_job

```
get_job(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.job.GetJobRequest, dict]
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
) -> google.cloud.run_v2.types.job.Job
```


Gets information about a Job.

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
def sample_get_job():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[GetJobRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_get_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for obtaining a Job by its full name. |
`name` |
`str`
Required. The full name of the Job. Format: projects/{project}/locations/{location}/jobs/{job}, where {project} can be project id or number. This corresponds to the |
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
Job represents the configuration of a single job, which references a container image that is run to completion. |

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

### job_path

`job_path(project: str, location: str, job: str) -> str`


Returns a fully-qualified job string.

### list_jobs

```
list_jobs(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.job.ListJobsRequest, dict]
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
) -> google.cloud.run_v2.services.jobs.pagers.ListJobsPager
```


Lists Jobs. Results are sorted by creation time, descending.

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
def sample_list_jobs():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[ListJobsRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_jobs](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_list_jobs)(request=request)
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
The request object. Request message for retrieving a list of Jobs. |
`parent` |
`str`
Required. The location and project to list resources on. Format: projects/{project}/locations/{location}, where {project} can be project id or number. This corresponds to the |
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
Response message containing a list of Jobs. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_policy_path

`parse_policy_path(path: str) -> typing.Dict[str, str]`


Parses a policy path into its component segments.

### parse_secret_path

`parse_secret_path(path: str) -> typing.Dict[str, str]`


Parses a secret path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### policy_path

`policy_path(project: str) -> str`


Returns a fully-qualified policy string.

### run_job

```
run_job(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.job.RunJobRequest, dict]
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


Triggers creation of a new Execution of this Job.

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
def sample_run_job():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[RunJobRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[run_job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_run_job)(request=request)
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
The request object. Request message to create a new Execution of a Job. |
`name` |
`str`
Required. The full name of the Job. Format: projects/{project}/locations/{location}/jobs/{job}, where {project} can be project id or number. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM Access control policy for the specified Job. Overwrites any existing policy.

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
def sample_set_iam_policy():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = iam_policy_pb2.SetIamPolicyRequest(
resource="resource_value",
)
# Make the request
response = client.[set_iam_policy](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_set_iam_policy)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_test_iam_permissions():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
request = iam_policy_pb2.TestIamPermissionsRequest(
resource="resource_value",
permissions=['permissions_value1', 'permissions_value2'],
)
# Make the request
response = client.[test_iam_permissions](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_test_iam_permissions)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
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
Response message for TestIamPermissions method. |

### update_job

```
update_job(
request: typing.Optional[
typing.Union[google.cloud.run_v2.types.job.UpdateJobRequest, dict]
] = None,
*,
job: typing.Optional[google.cloud.run_v2.types.job.Job] = None,
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


Updates a Job.

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
def sample_update_job():
# Create a client
client = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[JobsClient](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html)()
# Initialize request argument(s)
job = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[Job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job.html)()
job.start_execution_token = "start_execution_token_value"
job.template.template.max_retries = 1187
request = [run_v2](https://docs.cloud.google.com/python/docs/reference/run/latest).[UpdateJobRequest](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateJobRequest.html)(
job=job,
)
# Make the request
operation = client.[update_job](https://docs.cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.JobsClient.html#google_cloud_run_v2_services_jobs_JobsClient_update_job)(request=request)
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
The request object. Request message for updating a Job. |
`job` |
Required. The Job to be updated. This corresponds to the |
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