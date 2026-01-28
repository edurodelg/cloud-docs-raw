---
merged_at: 2026-01-28T15:11:44.782691
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient -->

# Class DeploymentResourcePoolServiceClient (1.135.0)

```
DeploymentResourcePoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
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
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.CreateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool.DeploymentResourcePool
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
from google.cloud import aiplatform_v1beta1
def sample_create_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1beta1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[CreateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolRequest.html)(
parent="parent_value",
deployment_resource_pool=deployment_resource_pool,
deployment_resource_pool_id="deployment_resource_pool_id_value",
)
# Make the request
operation = client.[create_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_create_deployment_resource_pool)(request=request)
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.DeleteDeploymentResourcePoolRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_delete_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_delete_deployment_resource_pool)(request=request)
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.GetDeploymentResourcePoolRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool.DeploymentResourcePool
)
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
from google.cloud import aiplatform_v1beta1
def sample_get_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_get_deployment_resource_pool)(request=request)
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
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
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_deployment_resource_pools():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDeploymentResourcePoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_deployment_resource_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_list_deployment_resource_pools)(request=request)
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
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
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager
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
from google.cloud import aiplatform_v1beta1
def sample_query_deployed_models():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[QueryDeployedModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsRequest.html)(
deployment_resource_pool="deployment_resource_pool_value",
)
# Make the request
page_result = client.[query_deployed_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_query_deployed_models)(request=request)
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.UpdateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool.DeploymentResourcePool
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
from google.cloud import aiplatform_v1beta1
def sample_update_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1beta1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[UpdateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolRequest.html)(
deployment_resource_pool=deployment_resource_pool,
)
# Make the request
operation = client.[update_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_update_deployment_resource_pool)(request=request)
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextExtractionPredictionInstance -->

# Class TextExtractionPredictionInstance (1.135.0)

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The text snippet to make the predictions on. |
`mime_type` |
`str`
The MIME type of the text snippet. The supported MIME types are listed below. - text/plain |
`key` |
`str`
This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Vertex AI will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique. |

## Methods

### TextExtractionPredictionInstance

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

### TextExtractionPredictionInstance

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesArrayFilter.ArrayOperator -->

# Class ArrayOperator (1.135.0)

`ArrayOperator(value)`


The logic to use for filtering.

## Enums |
|
|---|---|
Name |
Description |
`ARRAY_OPERATOR_UNSPECIFIED` |
Not specified. This value should not be used. |
`CONTAINS_ANY` |
The metadata array field in the example must contain at least one of the values. |
`CONTAINS_ALL` |
The metadata array field in the example must contain all of the values. |

## Methods

### ArrayOperator

`ArrayOperator(value)`


The logic to use for filtering.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeExecutionsMetadata -->

# Class PurgeExecutionsMetadata (1.135.0)

`PurgeExecutionsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeExecutions.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for purging Executions. |

## Methods

### PurgeExecutionsMetadata

`PurgeExecutionsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeExecutions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Metric.AggregationMetric -->

# Class AggregationMetric (1.135.0)

`AggregationMetric(value)`


The aggregation metrics supported by EvaluationService.EvaluateDataset.

## Enums |
|
|---|---|
Name |
Description |
`AGGREGATION_METRIC_UNSPECIFIED` |
Unspecified aggregation metric. |
`AVERAGE` |
Average aggregation metric. Not supported for Pairwise metric. |
`MODE` |
Mode aggregation metric. |
`STANDARD_DEVIATION` |
Standard deviation aggregation metric. Not supported for pairwise metric. |
`VARIANCE` |
Variance aggregation metric. Not supported for pairwise metric. |
`MINIMUM` |
Minimum aggregation metric. Not supported for pairwise metric. |
`MAXIMUM` |
Maximum aggregation metric. Not supported for pairwise metric. |
`MEDIAN` |
Median aggregation metric. Not supported for pairwise metric. |
`PERCENTILE_P90` |
90th percentile aggregation metric. Not supported for pairwise metric. |
`PERCENTILE_P95` |
95th percentile aggregation metric. Not supported for pairwise metric. |
`PERCENTILE_P99` |
99th percentile aggregation metric. Not supported for pairwise metric. |

## Methods

### AggregationMetric

`AggregationMetric(value)`


The aggregation metrics supported by EvaluationService.EvaluateDataset.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetCustomJobRequest -->

# Class GetCustomJobRequest (1.135.0)

`GetCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob resource. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### GetCustomJobRequest

`GetCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetCustomJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataOperationMetadata -->

# Class ImportDataOperationMetadata (1.135.0)

`ImportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ImportData.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### ImportDataOperationMetadata

`ImportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ImportData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteStudyRequest -->

# Class DeleteStudyRequest (1.135.0)

`DeleteStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteStudy.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Study resource to be deleted. Format: `projects/{project}/locations/{location}/studies/{study}`
|

## Methods

### DeleteStudyRequest

`DeleteStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteStudy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionResults -->

# Class TrajectoryPrecisionResults (1.135.0)

`TrajectoryPrecisionResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryPrecision metric.

## Attribute |
|
|---|---|
Name |
Description |
`trajectory_precision_metric_values` |
`MutableSequence[`
Output only. TrajectoryPrecision metric values. |

## Methods

### TrajectoryPrecisionResults

`TrajectoryPrecisionResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryPrecision metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureOperationMetadata -->

# Class CreateFeatureOperationMetadata (1.135.0)

```
CreateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Feature.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Feature. |

## Methods

### CreateFeatureOperationMetadata

```
CreateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchEntryPoint -->

# Class SearchEntryPoint (1.135.0)

`SearchEntryPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google search entry point.

## Attributes |
|
|---|---|
Name |
Description |
`rendered_content` |
`str`
Optional. Web content snippet that can be embedded in a web page or an app webview. |
`sdk_blob` |
`bytes`
Optional. Base64 encoded JSON representing array of |

## Methods

### SearchEntryPoint

`SearchEntryPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google search entry point.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationHelpfulnessResult -->

# Class SummarizationHelpfulnessResult (1.135.0)

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization helpfulness score. |
`confidence` |
`float`
Output only. Confidence for summarization helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationHelpfulnessResult

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionCallingConfig.Mode -->

# Class Mode (1.135.0)

`Mode(value)`


Function calling mode.

## Enums |
|
|---|---|
Name |
Description |
`MODE_UNSPECIFIED` |
Unspecified function calling mode. This value should not be used. |
`AUTO` |
Default model behavior, model decides to predict either function calls or natural language response. |
`ANY` |
Model is constrained to always predicting function calls only. If `allowed_function_names][FunctionCallingConfig.allowed_function_names]` are set, the predicted function calls will be limited to any one of `allowed_function_names`, else the predicted function calls will be any one of the provided [FunctionDeclaration]. |
`NONE` |
Model will not predict any function calls. Model behavior is same as when not passing any function declarations. |
`VALIDATED` |
Model is constrained to predict either function calls or natural language response. If `allowed_function_names][FunctionCallingConfig.allowed_function_names]` are set, the predicted function calls will be limited to any one of `allowed_function_names`, else the predicted function calls will be any one of the provided [FunctionDeclaration]. |

## Methods

### Mode

`Mode(value)`


Function calling mode.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureViewRequest -->

# Class CreateFeatureViewRequest (1.135.0)

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`feature_view` |
Required. The FeatureView to create. |
`feature_view_id` |
`str`
Required. The ID to use for the FeatureView, which will become the final component of the FeatureView's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within a FeatureOnlineStore.
|
`run_sync_immediately` |
`bool`
Immutable. If set to true, one on demand sync will be run immediately, regardless whether the FeatureView.sync_config is configured or not. |

## Methods

### CreateFeatureViewRequest

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureGroupRequest -->

# Class UpdateFeatureGroupRequest (1.135.0)

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group` |
Required. The FeatureGroup's `name` field is used to
identify the FeatureGroup to be updated. Format:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `description`
- `big_query`
- `big_query.entity_id_columns`
|

## Methods

### UpdateFeatureGroupRequest

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ServiceAccountSpec -->

# Class ServiceAccountSpec (1.135.0)

`ServiceAccountSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the use of custom service account to run the workloads.

## Attributes |
|
|---|---|
Name |
Description |
`enable_custom_service_account` |
`bool`
Required. If true, custom user-managed service account is enforced to run any workloads (for example, Vertex Jobs) on the resource. Otherwise, uses the `Vertex AI Custom Code Service Agent |
`service_account` |
`str`
Optional. Required when all below conditions are met - `enable_custom_service_account` is true;
- any runtime is specified via `ResourceRuntimeSpec` on
creation time, for example, Ray
The users must have `iam.serviceAccounts.actAs` permission
on this service account and then the specified runtime
containers will run as it.
Do not set this field if you want to submit jobs using
custom service account to this PersistentResource after
creation, but only specify the `service_account` inside
the job.
|

## Methods

### ServiceAccountSpec

`ServiceAccountSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the use of custom service account to run the workloads.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingReadFeatureValuesRequest -->

# Class StreamingReadFeatureValuesRequest (1.135.0)

```
StreamingReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the entities' type. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_ids` |
`MutableSequence[str]`
Required. IDs of entities to read Feature values of. The maximum number of IDs is 100. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. Feature IDs will be deduplicated. |

## Methods

### StreamingReadFeatureValuesRequest

```
StreamingReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchSpec -->

# Class ToolParameterKVMatchSpec (1.135.0)

`ToolParameterKVMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key value match metric.

## Attribute |
|
|---|---|
Name |
Description |
`use_strict_string_match` |
`bool`
Optional. Whether to use STRICT string match on parameter values. |

## Methods

### ToolParameterKVMatchSpec

`ToolParameterKVMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key value match metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest.Model -->

# Class Model (1.135.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the backend deployed model.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Optional. The model that the user will send the augmented prompt for content generation. |
`model_version` |
`str`
Optional. The model version of the backend deployed model. |

## Methods

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the backend deployed model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEndpointRequest -->

# Class GetEndpointRequest (1.135.0)

`GetEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.GetEndpoint

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Endpoint resource. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|

## Methods

### GetEndpointRequest

`GetEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.GetEndpoint

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteCachedContentRequest -->

# Class DeleteCachedContentRequest (1.135.0)

`DeleteCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.DeleteCachedContent.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name referring to the cached content |

## Methods

### DeleteCachedContentRequest

`DeleteCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.DeleteCachedContent.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelRequest -->

# Class DeleteModelRequest (1.135.0)

`DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.DeleteModel.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Model resource to be deleted. Format: `projects/{project}/locations/{location}/models/{model}`
|

## Methods

### DeleteModelRequest

`DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.DeleteModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Execution.State -->

# Class State (1.135.0)

`State(value)`


Describes the state of the Execution.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified Execution state |
`NEW` |
The Execution is new |
`RUNNING` |
The Execution is running |
`COMPLETE` |
The Execution has finished running |
`FAILED` |
The Execution has failed |
`CACHED` |
The Execution completed through Cache hit. |
`CANCELLED` |
The Execution was cancelled. |

## Methods

### State

`State(value)`


Describes the state of the Execution.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessResult -->

# Class SummarizationHelpfulnessResult (1.135.0)

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization helpfulness score. |
`confidence` |
`float`
Output only. Confidence for summarization helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationHelpfulnessResult

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringQualityResult -->

# Class QuestionAnsweringQualityResult (1.135.0)

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Quality score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringQualityResult

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EnterpriseWebSearch -->

# Class EnterpriseWebSearch (1.135.0)

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### EnterpriseWebSearch

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ErrorAnalysisAnnotation -->

# Class ErrorAnalysisAnnotation (1.135.0)

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.

## Attributes |
|
|---|---|
Name |
Description |
`attributed_items` |
`MutableSequence[`
Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type. |
`query_type` |
The query type used for finding the attributed items. |
`outlier_score` |
`float`
The outlier score of this annotated item. Usually defined as the min of all distances from attributed items. |
`outlier_threshold` |
`float`
The threshold used to determine if this annotation is an outlier or not. |

## Classes

### AttributedItem

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

### QueryType

`QueryType(value)`


The query type used for finding the attributed items.

## Methods

### ErrorAnalysisAnnotation

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupRequest -->

# Class UpdateFeatureGroupRequest (1.135.0)

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group` |
Required. The FeatureGroup's `name` field is used to
identify the FeatureGroup to be updated. Format:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `description`
- `big_query`
- `big_query.entity_id_columns`
|

## Methods

### UpdateFeatureGroupRequest

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexRequest -->

# Class DeleteIndexRequest (1.135.0)

`DeleteIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.DeleteIndex.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Index resource to be deleted. Format: `projects/{project}/locations/{location}/indexes/{index}`
|

## Methods

### DeleteIndexRequest

`DeleteIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.DeleteIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.Range -->

# Class Range (1.135.0)

`Range(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A range of values for slice(s). `low`

is inclusive, `high`

is
exclusive.

## Attributes |
|
|---|---|
Name |
Description |
`low` |
`float`
Inclusive low value for the range. |
`high` |
`float`
Exclusive high value for the range. |

## Methods

### Range

`Range(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A range of values for slice(s). `low`

is inclusive, `high`

is
exclusive.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetScheduleRequest -->

# Class GetScheduleRequest (1.135.0)

`GetScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.GetSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### GetScheduleRequest

`GetScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.GetSchedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DestinationFeatureSetting -->

# Class DestinationFeatureSetting (1.135.0)

`DestinationFeatureSetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`feature_id` |
`str`
Required. The ID of the Feature to apply the setting to. |
`destination_field` |
`str`
Specify the field name in the export destination. If not specified, Feature ID is used. |

## Methods

### DestinationFeatureSetting

`DestinationFeatureSetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsResponse -->

# Class ReadIndexDatapointsResponse (1.135.0)

`ReadIndexDatapointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.ReadIndexDatapoints.

## Attribute |
|
|---|---|
Name |
Description |
`datapoints` |
`MutableSequence[`
The result list of datapoints. |

## Methods

### ReadIndexDatapointsResponse

`ReadIndexDatapointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.ReadIndexDatapoints.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagEngineConfig -->

# Class RagEngineConfig (1.135.0)

`RagEngineConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for RagEngine.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The name of the RagEngineConfig. Format: `projects/{project}/locations/{location}/ragEngineConfig`
|
`rag_managed_db_config` |
The config of the RagManagedDb used by RagEngine. |

## Methods

### RagEngineConfig

`RagEngineConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for RagEngine.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis -->

# Class ImportFeaturesAnalysis (1.135.0)

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

## Attributes |
|
|---|---|
Name |
Description |
`state` |
Whether to enable / disable / inherite default hebavior for import features analysis. |
`anomaly_detection_baseline` |
The baseline used to do anomaly detection for the statistics generated by import features analysis. |

## Classes

### Baseline

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Methods

### ImportFeaturesAnalysis

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingReadFeatureValuesRequest -->

# Class StreamingReadFeatureValuesRequest (1.135.0)

```
StreamingReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the entities' type. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_ids` |
`MutableSequence[str]`
Required. IDs of entities to read Feature values of. The maximum number of IDs is 100. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. Feature IDs will be deduplicated. |

## Methods

### StreamingReadFeatureValuesRequest

```
StreamingReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextExtractionPredictionInstance -->

# Class TextExtractionPredictionInstance (1.135.0)

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The text snippet to make the predictions on. |
`mime_type` |
`str`
The MIME type of the text snippet. The supported MIME types are listed below. - text/plain |
`key` |
`str`
This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Vertex AI will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique. |

## Methods

### TextExtractionPredictionInstance

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

### TextExtractionPredictionInstance

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCustomJobRequest -->

# Class GetCustomJobRequest (1.135.0)

`GetCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob resource. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### GetCustomJobRequest

`GetCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetCustomJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNasJobRequest -->

# Class DeleteNasJobRequest (1.135.0)

`DeleteNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob resource to be deleted. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### DeleteNasJobRequest

`DeleteNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteNasJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitorJob.JobSummary -->

# Class JobSummary (1.135.0)

`JobSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the FeatureMonitorJob.

## Attributes |
|
|---|---|
Name |
Description |
`total_slot_ms` |
`int`
Output only. BigQuery slot milliseconds consumed. |
`feature_stats_and_anomalies` |
`MutableSequence[`
Output only. Features and their stats and anomalies |

## Methods

### JobSummary

`JobSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the FeatureMonitorJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SampleConfig.SampleStrategy -->

# Class SampleStrategy (1.135.0)

`SampleStrategy(value)`


Sample strategy decides which subset of DataItems should be selected for human labeling in every batch.

## Enums |
|
|---|---|
Name |
Description |
`SAMPLE_STRATEGY_UNSPECIFIED` |
Default will be treated as UNCERTAINTY. |
`UNCERTAINTY` |
Sample the most uncertain data to label. |

## Methods

### SampleStrategy

`SampleStrategy(value)`


Sample strategy decides which subset of DataItems should be selected for human labeling in every batch.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest -->

# Class DeleteFeatureValuesRequest (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig.TtlConfig.GranularTtlConfig -->

# Class GranularTtlConfig (1.135.0)

`GranularTtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.

## Attributes |
|
|---|---|
Name |
Description |
`create_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The TTL duration for memories uploaded via CreateMemory. |
`generate_created_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The TTL duration for memories newly generated via GenerateMemories (GenerateMemoriesResponse.GeneratedMemory.Action.CREATED). |
`generate_updated_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The TTL duration for memories updated via GenerateMemories (GenerateMemoriesResponse.GeneratedMemory.Action.CREATED). In the case of an UPDATE action, the `expire_time` of the
existing memory will be updated to the new value (now +
TTL).
|

## Methods

### GranularTtlConfig

`GranularTtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetDistribution -->

# Class DatasetDistribution (1.135.0)

`DatasetDistribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Distribution computed over a tuning dataset.

## Attributes |
|
|---|---|
Name |
Description |
`sum` |
`float`
Output only. Sum of a given population of values. |
`min_` |
`float`
Output only. The minimum of the population values. |
`max_` |
`float`
Output only. The maximum of the population values. |
`mean` |
`float`
Output only. The arithmetic mean of the values in the population. |
`median` |
`float`
Output only. The median of the values in the population. |
`p5` |
`float`
Output only. The 5th percentile of the values in the population. |
`p95` |
`float`
Output only. The 95th percentile of the values in the population. |
`buckets` |
`MutableSequence[`
Output only. Defines the histogram bucket. |

## Classes

### DistributionBucket

`DistributionBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Methods

### DatasetDistribution

`DatasetDistribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Distribution computed over a tuning dataset.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient -->

# Class PersistentResourceServiceAsyncClient (1.135.0)

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
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
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
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
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
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
from google.cloud import aiplatform_v1beta1
async def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_create_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.DeletePersistentResourceRequest,
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
from google.cloud import aiplatform_v1beta1
async def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_delete_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.GetPersistentResourceRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
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
from google.cloud import aiplatform_v1beta1
async def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_get_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport
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
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
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
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_list_persistent_resources)(request=request)
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
The request object. Request message for [PersistentResourceService.ListPersistentResource][]. |
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

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

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
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.RebootPersistentResourceRequest,
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
from google.cloud import aiplatform_v1beta1
async def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_reboot_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
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
from google.cloud import aiplatform_v1beta1
async def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_update_persistent_resource)(request=request)
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOperationMetadata -->

# Class CreateFeatureOperationMetadata (1.135.0)

```
CreateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Feature.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Feature. |

## Methods

### CreateFeatureOperationMetadata

```
CreateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataOperationMetadata -->

# Class ImportDataOperationMetadata (1.135.0)

`ImportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ImportData.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### ImportDataOperationMetadata

`ImportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ImportData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteStudyRequest -->

# Class DeleteStudyRequest (1.135.0)

`DeleteStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteStudy.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Study resource to be deleted. Format: `projects/{project}/locations/{location}/studies/{study}`
|

## Methods

### DeleteStudyRequest

`DeleteStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.DeleteStudy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchEntryPoint -->

# Class SearchEntryPoint (1.135.0)

`SearchEntryPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google search entry point.

## Attributes |
|
|---|---|
Name |
Description |
`rendered_content` |
`str`
Optional. Web content snippet that can be embedded in a web page or an app webview. |
`sdk_blob` |
`bytes`
Optional. Base64 encoded JSON representing array of |

## Methods

### SearchEntryPoint

`SearchEntryPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google search entry point.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringBigQueryTable -->

# Class ModelDeploymentMonitoringBigQueryTable (1.135.0)

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

## Attributes |
|
|---|---|
Name |
Description |
`log_source` |
The source of log. |
`log_type` |
The type of log. |
`bigquery_table_path` |
`str`
The created BigQuery table to store logs. Customer could do their own query & analysis. Format: `bq://`
|
`request_response_logging_schema_version` |
`str`
Output only. The schema version of the request/response logging BigQuery table. Default to v1 if unset. |

## Classes

### LogSource

`LogSource(value)`


Indicates where does the log come from.

### LogType

`LogType(value)`


Indicates what type of traffic does the log belong to.

## Methods

### ModelDeploymentMonitoringBigQueryTable

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorRequest -->

# Class UpdateFeatureMonitorRequest (1.135.0)

`UpdateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureMonitor.

## Attributes |
|
|---|---|
Name |
Description |
`feature_monitor` |
Required. The FeatureMonitor's `name` field is used to
identify the FeatureMonitor to be updated. Format:
`projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to specify the fields to be overwritten in the FeatureMonitor resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
|

## Methods

### UpdateFeatureMonitorRequest

`UpdateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureMonitor.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardSizeResponse -->

# Class ReadTensorboardSizeResponse (1.135.0)

`ReadTensorboardSizeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ReadTensorboardSize.

## Attribute |
|
|---|---|
Name |
Description |
`storage_size_byte` |
`int`
Payload storage size for the TensorBoard |

## Methods

### ReadTensorboardSizeResponse

`ReadTensorboardSizeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ReadTensorboardSize.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.ExplanationConfig.ExplanationBaseline.PredictionFormat -->

# Class PredictionFormat (1.135.0)

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

## Enums |
|
|---|---|
Name |
Description |
`PREDICTION_FORMAT_UNSPECIFIED` |
Should not be set. |
`JSONL` |
Predictions are in JSONL files. |
`BIGQUERY` |
Predictions are in BigQuery. |

## Methods

### PredictionFormat

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ErrorAnalysisAnnotation -->

# Class ErrorAnalysisAnnotation (1.135.0)

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.

## Attributes |
|
|---|---|
Name |
Description |
`attributed_items` |
`MutableSequence[`
Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type. |
`query_type` |
The query type used for finding the attributed items. |
`outlier_score` |
`float`
The outlier score of this annotated item. Usually defined as the min of all distances from attributed items. |
`outlier_threshold` |
`float`
The threshold used to determine if this annotation is an outlier or not. |

## Classes

### AttributedItem

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

### QueryType

`QueryType(value)`


The query type used for finding the attributed items.

## Methods

### ErrorAnalysisAnnotation

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionInstance -->

# Class TrajectoryPrecisionInstance (1.135.0)

`TrajectoryPrecisionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryPrecision instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|
`reference_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for reference tool call trajectory. This field is a member of `oneof` _ `_reference_trajectory` .
|

## Methods

### TrajectoryPrecisionInstance

`TrajectoryPrecisionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryPrecision instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighbors -->

# Class NearestNeighbors (1.135.0)

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

## Attribute |
|
|---|---|
Name |
Description |
`neighbors` |
`MutableSequence[`
All its neighbors. |

## Classes

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Methods

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataOperationMetadata -->

# Class AssessDataOperationMetadata (1.135.0)

`AssessDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.AssessData.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### AssessDataOperationMetadata

`AssessDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.AssessData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityResult -->

# Class QuestionAnsweringQualityResult (1.135.0)

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Quality score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringQualityResult

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EnterpriseWebSearch -->

# Class EnterpriseWebSearch (1.135.0)

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### EnterpriseWebSearch

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest -->

# Class DeleteFeatureValuesRequest (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPublisherModelRequest -->

# Class GetPublisherModelRequest (1.135.0)

`GetPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.GetPublisherModel

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}`
|
`language_code` |
`str`
Optional. The IETF BCP-47 language code representing the language in which the publisher model's text information should be written in. |
`view` |
Optional. PublisherModel view specifying which fields to read. |
`is_hugging_face_model` |
`bool`
Optional. Boolean indicates whether the requested model is a Hugging Face model. |
`hugging_face_token` |
`str`
Optional. Token used to access Hugging Face gated models. |
`include_equivalent_model_garden_model_deployment_configs` |
`bool`
Optional. Whether to cnclude the deployment configs from the equivalent Model Garden model if the requested model is a Hugging Face model. |

## Methods

### GetPublisherModelRequest

`GetPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.GetPublisherModel

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/summary_overview -->

# AI Platform API

Overview of the APIs available for AI Platform API.

## All entries

Classes, methods and properties & attributes for AI Platform API.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.RagManagedDb.KNN -->

# Class KNN (1.135.0)

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

## Methods

### KNN

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDataKey.CompositeKey -->

# Class CompositeKey (1.135.0)

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

## Attribute |
|
|---|---|
Name |
Description |
`parts` |
`MutableSequence[str]`
Parts to construct Entity ID. Should match with the same ID columns as defined in FeatureView in the same order. |

## Methods

### CompositeKey

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis -->

# Class ImportFeaturesAnalysis (1.135.0)

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

## Attributes |
|
|---|---|
Name |
Description |
`state` |
Whether to enable / disable / inherite default hebavior for import features analysis. |
`anomaly_detection_baseline` |
The baseline used to do anomaly detection for the statistics generated by import features analysis. |

## Classes

### Baseline

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Methods

### ImportFeaturesAnalysis

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAnomaly -->

# Class ModelMonitoringAnomaly (1.135.0)

`ModelMonitoringAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single model monitoring anomaly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`tabular_anomaly` |
Tabular anomaly. This field is a member of `oneof` _ `anomaly` .
|
`model_monitoring_job` |
`str`
Model monitoring job resource name. |
`algorithm` |
`str`
Algorithm used to calculated the metrics, eg: jensen_shannon_divergence, l_infinity. |

## Classes

### TabularAnomaly

`TabularAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular anomaly details.

## Methods

### ModelMonitoringAnomaly

`ModelMonitoringAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single model monitoring anomaly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob -->

# Class BatchPredictionJob (1.135.0)

`BatchPredictionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.

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
Required. Input configuration of the instances on which predictions are performed. The schema of any single instance may be specified via the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`instance_config` |
Configuration for how to convert batch prediction input instances to the prediction instances that are sent to the Model. |
`model_parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the predictions. The schema of the parameters may be specified via the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. |
`output_config` |
Required. The Configuration specifying where output predictions should be written. The schema of any single prediction may be specified as a concatenation of [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri and prediction_schema_uri. |
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
the
Explanation
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
`model_monitoring_config` |
Model monitoring config will be used for analysis model behaviors, based on the input and output to the batch prediction job, as well as the provided training dataset. |
`model_monitoring_stats_anomalies` |
`MutableSequence[`
Get batch prediction job monitoring statistics. |
`model_monitoring_status` |
`google.rpc.status_pb2.Status`
Output only. The running status of the model monitoring pipeline. |
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


A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingRawPredictRequest -->

# Class StreamingRawPredictRequest (1.135.0)

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### StreamingRawPredictRequest

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardTimeSeriesRequest -->

# Class UpdateTensorboardTimeSeriesRequest (1.135.0)

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardTimeSeries resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries' `name` field is used
to identify the TensorboardTimeSeries to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### UpdateTensorboardTimeSeriesRequest

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec.InlineSource -->

# Class InlineSource (1.135.0)

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

## Attribute |
|
|---|---|
Name |
Description |
`source_archive` |
`bytes`
Required. Input only. The application source code archive, provided as a compressed tarball (.tar.gz) file. |

## Methods

### InlineSource

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCachedContentRequest -->

# Class DeleteCachedContentRequest (1.135.0)

`DeleteCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.DeleteCachedContent.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name referring to the cached content |

## Methods

### DeleteCachedContentRequest

`DeleteCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.DeleteCachedContent.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringBigQueryTable -->

# Class ModelDeploymentMonitoringBigQueryTable (1.135.0)

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

## Attributes |
|
|---|---|
Name |
Description |
`log_source` |
The source of log. |
`log_type` |
The type of log. |
`bigquery_table_path` |
`str`
The created BigQuery table to store logs. Customer could do their own query & analysis. Format: `bq://`
|
`request_response_logging_schema_version` |
`str`
Output only. The schema version of the request/response logging BigQuery table. Default to v1 if unset. |

## Classes

### LogSource

`LogSource(value)`


Indicates where does the log come from.

### LogType

`LogType(value)`


Indicates what type of traffic does the log belong to.

## Methods

### ModelDeploymentMonitoringBigQueryTable

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureOperationMetadata -->

# Class UpdateFeatureOperationMetadata (1.135.0)

```
UpdateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Feature.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Feature Update. |

## Methods

### UpdateFeatureOperationMetadata

```
UpdateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectPredictResponse -->

# Class DirectPredictResponse (1.135.0)

`DirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectPredict.

## Attributes |
|
|---|---|
Name |
Description |
`outputs` |
`MutableSequence[`
The prediction output. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### DirectPredictResponse

`DirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectPredict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureGroup.BigQuery.TimeSeries -->

# Class TimeSeries (1.135.0)

`TimeSeries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`timestamp_column` |
`str`
Optional. Column hosting timestamp values for a time-series source. Will be used to determine the latest `feature_values` for each entity. Optional. If not
provided, column named `feature_timestamp` of type
`TIMESTAMP` will be used.
|

## Methods

### TimeSeries

`TimeSeries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEngineConfig -->

# Class RagEngineConfig (1.135.0)

`RagEngineConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for RagEngine.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The name of the RagEngineConfig. Format: `projects/{project}/locations/{location}/ragEngineConfig`
|
`rag_managed_db_config` |
The config of the RagManagedDb used by RagEngine. |

## Methods

### RagEngineConfig

`RagEngineConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for RagEngine.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationSpec -->

# Class ExplanationSpec (1.135.0)

`ExplanationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of Model explanation.

## Attributes |
|
|---|---|
Name |
Description |
`parameters` |
Required. Parameters that configure explaining of the Model's predictions. |
`metadata` |
Optional. Metadata describing the Model's input and output for explanation. |

## Methods

### ExplanationSpec

`ExplanationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of Model explanation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service -->

# Package vertex_rag_service (1.135.0)

API documentation for `aiplatform_v1.services.vertex_rag_service`

package.

## Classes

[VertexRagServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient)

A service for retrieving relevant contexts.

[VertexRagServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceClient)

A service for retrieving relevant contexts.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Artifact.State -->

# Class State (1.135.0)

`State(value)`


Describes the state of the Artifact.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified state for the Artifact. |
`PENDING` |
A state used by systems like Vertex AI Pipelines to indicate that the underlying data item represented by this Artifact is being created. |
`LIVE` |
A state indicating that the Artifact should exist, unless something external to the system deletes it. |

## Methods

### State

`State(value)`


Describes the state of the Artifact.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BigQuerySource -->

# Class BigQuerySource (1.135.0)

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the input content.

## Attribute |
|
|---|---|
Name |
Description |
`input_uri` |
`str`
Required. BigQuery URI to a table, up to 2000 characters long. Accepted forms: - BigQuery path. For example: `bq://projectId.bqDatasetId.bqTableId` .
|

## Methods

### BigQuerySource

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the input content.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient -->

# Class DatasetServiceAsyncClient (1.135.0)

```
DatasetServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that manages Vertex AI Dataset and its child resources.

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
`DatasetServiceTransport` |
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

### DatasetServiceAsyncClient

```
DatasetServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the dataset service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DatasetServiceTransport,Callable[..., DatasetServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the DatasetServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotation_path

```
annotation_path(
project: str, location: str, dataset: str, data_item: str, annotation: str
) -> str
```


Returns a fully-qualified annotation string.

### annotation_spec_path

```
annotation_spec_path(
project: str, location: str, dataset: str, annotation_spec: str
) -> str
```


Returns a fully-qualified annotation_spec string.

### assemble_data

```
assemble_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.AssembleDataRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Assembles each row of a multimodal dataset and writes the result into a BigQuery table.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_assemble_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AssembleDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataRequest.html)(
name="name_value",
)
# Make the request
operation = client.[assemble_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_assemble_data)(request=request)
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
The request object. Request message for DatasetService.AssembleData. Used only for MULTIMODAL datasets. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### assess_data

```
assess_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.AssessDataRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Assesses the state or validity of the dataset with respect to a given use case.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_assess_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
tuning_validation_assessment_config = aiplatform_v1beta1.[TuningValidationAssessmentConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.TuningValidationAssessmentConfig.html)()
tuning_validation_assessment_config.model_name = "model_name_value"
tuning_validation_assessment_config.dataset_usage = "SFT_VALIDATION"
request = aiplatform_v1beta1.[AssessDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.html)(
tuning_validation_assessment_config=tuning_validation_assessment_config,
name="name_value",
)
# Make the request
operation = client.[assess_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_assess_data)(request=request)
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
The request object. Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### create_dataset

```
create_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.CreateDatasetRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.Dataset
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


Creates a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetRequest.html)(
parent="parent_value",
dataset=dataset,
)
# Make the request
operation = client.[create_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_create_dataset)(request=request)
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
The request object. Request message for DatasetService.CreateDataset. |
`parent` |
Required. The resource name of the Location to create the Dataset in. Format: |
`dataset` |
Required. The Dataset to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### create_dataset_version

```
create_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.CreateDatasetVersionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
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


Create a version from a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1beta1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetVersionRequest.html)(
parent="parent_value",
dataset_version=dataset_version,
)
# Make the request
operation = client.[create_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_create_dataset_version)(request=request)
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
The request object. Request message for DatasetService.CreateDatasetVersion. |
`parent` |
Required. The name of the Dataset resource. Format: |
`dataset_version` |
Required. The version to be created. The same CMEK policies with the original Dataset will be applied the dataset version. So here we don't need to specify the EncryptionSpecType here. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### data_item_path

`data_item_path(project: str, location: str, dataset: str, data_item: str) -> str`


Returns a fully-qualified data_item string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

### dataset_version_path

```
dataset_version_path(
project: str, location: str, dataset: str, dataset_version: str
) -> str
```


Returns a fully-qualified dataset_version string.

### delete_dataset

```
delete_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteDatasetRequest,
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


Deletes a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_delete_dataset)(request=request)
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
The request object. Request message for DatasetService.DeleteDataset. |
`name` |
Required. The resource name of the Dataset to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_dataset_version

```
delete_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteDatasetVersionRequest,
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


Deletes a Dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_delete_dataset_version)(request=request)
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
The request object. Request message for DatasetService.DeleteDatasetVersion. |
`name` |
Required. The resource name of the Dataset version to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_saved_query

```
delete_saved_query(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteSavedQueryRequest,
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


Deletes a SavedQuery.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_saved_query():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSavedQueryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSavedQueryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_saved_query](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_delete_saved_query)(request=request)
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
The request object. Request message for DatasetService.DeleteSavedQuery. |
`name` |
Required. The resource name of the SavedQuery to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### export_data

```
export_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ExportDataRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
export_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.ExportDataConfig
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


Exports data from a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_export_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
export_config = aiplatform_v1beta1.[ExportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig.html)()
export_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ExportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataRequest.html)(
name="name_value",
export_config=export_config,
)
# Make the request
operation = client.[export_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_export_data)(request=request)
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
The request object. Request message for DatasetService.ExportData. |
`name` |
Required. The name of the Dataset resource. Format: |
`export_config` |
Required. The desired output location. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`DatasetServiceAsyncClient` |
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
`DatasetServiceAsyncClient` |
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
`DatasetServiceAsyncClient` |
The constructed client. |

### get_annotation_spec

```
get_annotation_spec(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetAnnotationSpecRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.annotation_spec.AnnotationSpec
```


Gets an AnnotationSpec.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_annotation_spec():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetAnnotationSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_annotation_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_get_annotation_spec)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.GetAnnotationSpec. |
`name` |
Required. The name of the AnnotationSpec resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Identifies a concept with which DataItems may be annotated with. |

### get_dataset

```
get_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetDatasetRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.dataset.Dataset
```


Gets a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_get_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.GetDataset. |
`name` |
Required. The name of the Dataset resource. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A collection of DataItems and Annotations on them. |

### get_dataset_version

```
get_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetDatasetVersionRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
```


Gets a Dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_get_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.GetDatasetVersion. |
`name` |
Required. The resource name of the Dataset version to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Describes the dataset version. |

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
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport
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

### import_data

```
import_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ImportDataRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
import_configs: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.dataset.ImportDataConfig
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
) -> google.api_core.operation_async.AsyncOperation
```


Imports data into a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_import_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
import_configs = aiplatform_v1beta1.[ImportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.html)()
import_configs.gcs_source.uris = ['uris_value1', 'uris_value2']
import_configs.import_schema_uri = "import_schema_uri_value"
request = aiplatform_v1beta1.[ImportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataRequest.html)(
name="name_value",
import_configs=import_configs,
)
# Make the request
operation = client.[import_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_import_data)(request=request)
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
The request object. Request message for DatasetService.ImportData. |
`name` |
Required. The name of the Dataset resource. Format: |
`import_configs` |
`:class:`
Required. The desired input locations. The contents of all input locations will be imported in one batch. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### list_annotations

```
list_annotations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsAsyncPager
)
```


Lists Annotations belongs to a dataitem.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_annotations():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_list_annotations)(request=request)
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
The request object. Request message for DatasetService.ListAnnotations. |
`parent` |
Required. The resource name of the DataItem to list Annotations from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListAnnotations. Iterating over this object will yield results and resolve additional pages automatically. |

### list_data_items

```
list_data_items(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsAsyncPager
)
```


Lists DataItems in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_data_items():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_list_data_items)(request=request)
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
The request object. Request message for DatasetService.ListDataItems. |
`parent` |
Required. The resource name of the Dataset to list DataItems from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListDataItems. Iterating over this object will yield results and resolve additional pages automatically. |

### list_dataset_versions

```
list_dataset_versions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager
)
```


Lists DatasetVersions in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_dataset_versions():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDatasetVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_dataset_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_list_dataset_versions)(request=request)
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
The request object. Request message for DatasetService.ListDatasetVersions. |
`parent` |
Required. The resource name of the Dataset to list DatasetVersions from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListDatasetVersions. Iterating over this object will yield results and resolve additional pages automatically. |

### list_datasets

```
list_datasets(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsAsyncPager
)
```


Lists Datasets in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_datasets():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDatasetsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_datasets](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_list_datasets)(request=request)
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
The request object. Request message for DatasetService.ListDatasets. |
`parent` |
Required. The name of the Dataset's parent resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListDatasets. Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_saved_queries

```
list_saved_queries(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesAsyncPager
)
```


Lists SavedQueries in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_saved_queries():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSavedQueriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_saved_queries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_list_saved_queries)(request=request)
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
The request object. Request message for DatasetService.ListSavedQueries. |
`parent` |
Required. The resource name of the Dataset to list SavedQueries from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListSavedQueries. Iterating over this object will yield results and resolve additional pages automatically. |

### parse_annotation_path

`parse_annotation_path(path: str) -> typing.Dict[str, str]`


Parses a annotation path into its component segments.

### parse_annotation_spec_path

`parse_annotation_spec_path(path: str) -> typing.Dict[str, str]`


Parses a annotation_spec path into its component segments.

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

### parse_data_item_path

`parse_data_item_path(path: str) -> typing.Dict[str, str]`


Parses a data_item path into its component segments.

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_dataset_version_path

`parse_dataset_version_path(path: str) -> typing.Dict[str, str]`


Parses a dataset_version path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_saved_query_path

`parse_saved_query_path(path: str) -> typing.Dict[str, str]`


Parses a saved_query path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### restore_dataset_version

```
restore_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.RestoreDatasetVersionRequest,
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


Restores a dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_restore_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RestoreDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[restore_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_restore_dataset_version)(request=request)
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
The request object. Request message for DatasetService.RestoreDatasetVersion. |
`name` |
Required. The name of the DatasetVersion resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### saved_query_path

```
saved_query_path(
project: str, location: str, dataset: str, saved_query: str
) -> str
```


Returns a fully-qualified saved_query string.

### search_data_items

```
search_data_items(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
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
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsAsyncPager
)
```


Searches DataItems in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_search_data_items():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsRequest.html)(
order_by_data_item="order_by_data_item_value",
dataset="dataset_value",
)
# Make the request
page_result = client.[search_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_search_data_items)(request=request)
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
The request object. Request message for DatasetService.SearchDataItems. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.SearchDataItems. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_dataset

```
update_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.UpdateDatasetRequest,
dict,
]
] = None,
*,
dataset: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.Dataset
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
) -> google.cloud.aiplatform_v1beta1.types.dataset.Dataset
```


Updates a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[UpdateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetRequest.html)(
dataset=dataset,
)
# Make the request
response = await client.[update_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_update_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.UpdateDataset. |
`dataset` |
Required. The Dataset which replaces the resource on the server. This corresponds to the |
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
A collection of DataItems and Annotations on them. |

### update_dataset_version

```
update_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.UpdateDatasetVersionRequest,
dict,
]
] = None,
*,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
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
) -> google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
```


Updates a DatasetVersion.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1beta1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[UpdateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest.html)(
dataset_version=dataset_version,
)
# Make the request
response = await client.[update_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceAsyncClient_update_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.UpdateDatasetVersion. |
`dataset_version` |
Required. The DatasetVersion which replaces the resource on the server. This corresponds to the |
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
Describes the dataset version. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient -->

# Class DeploymentResourcePoolServiceAsyncClient (1.135.0)

```
DeploymentResourcePoolServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### DeploymentResourcePoolServiceAsyncClient

```
DeploymentResourcePoolServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the deployment resource pool service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the DeploymentResourcePoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[CreateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolRequest.html)(
parent="parent_value",
deployment_resource_pool=deployment_resource_pool,
deployment_resource_pool_id="deployment_resource_pool_id_value",
)
# Make the request
operation = client.[create_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_create_deployment_resource_pool)(request=request)
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
The request object. Request message for CreateDeploymentResourcePool method. |
`parent` |
Required. The parent location resource where this DeploymentResourcePool will be created. Format: |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. This corresponds to the |
`deployment_resource_pool_id` |
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_delete_deployment_resource_pool)(request=request)
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
The request object. Request message for DeleteDeploymentResourcePool method. |
`name` |
Required. The name of the DeploymentResourcePool to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`DeploymentResourcePoolServiceAsyncClient` |
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
`DeploymentResourcePoolServiceAsyncClient` |
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
`DeploymentResourcePoolServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_get_deployment_resource_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GetDeploymentResourcePool method. |
`name` |
Required. The name of the DeploymentResourcePool to retrieve. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsAsyncPager
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
async def sample_list_deployment_resource_pools():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDeploymentResourcePoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_deployment_resource_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_list_deployment_resource_pools)(request=request)
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
The request object. Request message for ListDeploymentResourcePools method. |
`parent` |
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager
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
async def sample_query_deployed_models():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryDeployedModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsRequest.html)(
deployment_resource_pool="deployment_resource_pool_value",
)
# Make the request
page_result = client.[query_deployed_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_query_deployed_models)(request=request)
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
The request object. Request message for QueryDeployedModels method. |
`deployment_resource_pool` |
Required. The name of the target DeploymentResourcePool to query. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_update_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[UpdateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDeploymentResourcePoolRequest.html)(
deployment_resource_pool=deployment_resource_pool,
)
# Make the request
operation = client.[update_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_update_deployment_resource_pool)(request=request)
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
The request object. Request message for UpdateDeploymentResourcePool method. |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to update. The DeploymentResourcePool's |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelsPager -->

# Class ListModelsPager (1.135.0)

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModels`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelsPager

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictRequest -->

# Class StreamingRawPredictRequest (1.135.0)

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### StreamingRawPredictRequest

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.PredictionHandler -->

# Class PredictionHandler (1.135.0)

```
PredictionHandler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Default prediction handler for the prediction requests sent to the application.

## Methods

### PredictionHandler

```
PredictionHandler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Initializes a Handler instance.

Parameters |
|
|---|---|
Name |
Description |
`artifacts_uri` |
`str`
Required. The value of the environment variable AIP_STORAGE_URI. |
`predictor` |
`Type[Predictor]`
Optional. The Predictor class this handler uses to initiate predictor instance if given. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If predictor is None. |

### handle

`handle(request: starlette.requests.Request) -> starlette.responses.Response`


Handles a prediction request.

Parameter |
|
|---|---|
Name |
Description |
`request` |
`Request`
Required. The prediction request sent to the application. |

Exceptions |
|
|---|---|
Type |
Description |
`HTTPException` |
If any exception is thrown from predictor object. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNasJobRequest -->

# Class DeleteNasJobRequest (1.135.0)

`DeleteNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob resource to be deleted. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### DeleteNasJobRequest

`DeleteNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteNasJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.ModelConfig -->

# Class ModelConfig (1.135.0)

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for model selection.

## Attribute |
|
|---|---|
Name |
Description |
`feature_selection_preference` |
Required. Feature selection preference. |

## Classes

### FeatureSelectionPreference

`FeatureSelectionPreference(value)`


Options for feature selection preference.

## Methods

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for model selection.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchResults -->

# Class TrajectoryExactMatchResults (1.135.0)

`TrajectoryExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryExactMatch metric.

## Attribute |
|
|---|---|
Name |
Description |
`trajectory_exact_match_metric_values` |
`MutableSequence[`
Output only. TrajectoryExactMatch metric values. |

## Methods

### TrajectoryExactMatchResults

`TrajectoryExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryExactMatch metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecResponse.Recommendation.QuotaState -->

# Class QuotaState (1.135.0)

`QuotaState(value)`


The user accelerator quota state.

## Enums |
|
|---|---|
Name |
Description |
`QUOTA_STATE_UNSPECIFIED` |
Unspecified quota state. Quota information not available. |
`QUOTA_STATE_USER_HAS_QUOTA` |
User has enough accelerator quota for the machine type. |
`QUOTA_STATE_NO_USER_QUOTA` |
User does not have enough accelerator quota for the machine type. |

## Methods

### QuotaState

`QuotaState(value)`


The user accelerator quota state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest -->

# Class DeployRequest (1.135.0)

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
`publisher_model_name` |
`str`
The Model Garden model to deploy. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` .
This field is a member of `oneof` _ `artifacts` .
|
`hugging_face_model_id` |
`str`
The Hugging Face model to deploy. Format: Hugging Face model ID like `google/gemma-2-2b-it` .
This field is a member of `oneof` _ `artifacts` .
|
`destination` |
`str`
Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`model_config` |
Optional. The model config to use for the deployment. If not specified, the default model config will be used. |
`endpoint_config` |
Optional. The endpoint config to use for the deployment. If not specified, the default endpoint config will be used. |
`deploy_config` |
Optional. The deploy config to use for the deployment. If not specified, the default deploy config will be used. |

## Classes

### DeployConfig

`DeployConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The deploy config to use for the deployment.

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Methods

### DeployRequest

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardTimeSeriesRequest -->

# Class UpdateTensorboardTimeSeriesRequest (1.135.0)

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardTimeSeries resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries' `name` field is used
to identify the TensorboardTimeSeries to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### UpdateTensorboardTimeSeriesRequest

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs.ModelType -->

# Class ModelType (1.135.0)

A model to be used via prediction calls to uCAIP API. Expected to have a higher latency, but should also have a higher prediction quality than other models.

CLOUD_LOW_ACCURACY_1

A model to be used via prediction calls to uCAIP API. Expected to have a lower latency but relatively lower prediction quality.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-28 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataResponse -->

# Class GenerateSyntheticDataResponse (1.135.0)

```
GenerateSyntheticDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The response containing the generated data.

## Attribute |
|
|---|---|
Name |
Description |
`synthetic_examples` |
`MutableSequence[`
A list of generated synthetic examples. |

## Methods

### GenerateSyntheticDataResponse

```
GenerateSyntheticDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The response containing the generated data.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.ExplanationConfig.ExplanationBaseline.PredictionFormat -->

# Class PredictionFormat (1.135.0)

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

## Enums |
|
|---|---|
Name |
Description |
`PREDICTION_FORMAT_UNSPECIFIED` |
Should not be set. |
`JSONL` |
Predictions are in JSONL files. |
`BIGQUERY` |
Predictions are in BigQuery. |

## Methods

### PredictionFormat

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardSizeResponse -->

# Class ReadTensorboardSizeResponse (1.135.0)

`ReadTensorboardSizeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ReadTensorboardSize.

## Attribute |
|
|---|---|
Name |
Description |
`storage_size_byte` |
`int`
Payload storage size for the TensorBoard |

## Methods

### ReadTensorboardSizeResponse

`ReadTensorboardSizeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ReadTensorboardSize.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighbors -->

# Class NearestNeighbors (1.135.0)

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

## Attribute |
|
|---|---|
Name |
Description |
`neighbors` |
`MutableSequence[`
All its neighbors. |

## Classes

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Methods

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping -->

# Class DatapointFieldMapping (1.135.0)

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.

## Attributes |
|
|---|---|
Name |
Description |
`id_column` |
`str`
Required. The column with unique identifiers for each data point. |
`embedding_column` |
`str`
Required. The column with the vector embeddings for each data point. |
`restricts` |
`MutableSequence[`
Optional. List of restricts for string values. |
`numeric_restricts` |
`MutableSequence[`
Optional. List of restricts for numeric values. |
`metadata_columns` |
`MutableSequence[str]`
Optional. List of columns containing metadata to be included in the index. |

## Classes

### NumericRestrict

`NumericRestrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on numeric values.

### Restrict

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.

## Methods

### DatapointFieldMapping

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.GoogleSearch -->

# Class GoogleSearch (1.135.0)

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: ["amazon.com", "facebook.com"]. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest -->

# Class MutateDeployedModelRequest (1.135.0)

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - `min_replica_count` in either
DedicatedResources
or
AutomaticResources
- `max_replica_count` in either
DedicatedResources
or
AutomaticResources
- `required_replica_count` in
DedicatedResources
- autoscaling_metric_specs
- `disable_container_logging` (v1 only)
- `enable_container_logging` (v1beta1 only)
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### MutateDeployedModelRequest

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest -->

# Class BatchCreateFeaturesRequest (1.135.0)

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each
child request message can be omitted. If `parent` is set
in a child request, then the value must match the `parent`
value in this request message.
|

## Methods

### BatchCreateFeaturesRequest

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsPager -->

# Class ListTrialsPager (1.135.0)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrialsPager

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsPager -->

# Class ListNasJobsPager (1.135.0)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasJobsPager

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileChunkingConfig -->

# Class RagFileChunkingConfig (1.135.0)

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`fixed_length_chunking` |
Specifies the fixed length chunking config. This field is a member of `oneof` _ `chunking_config` .
|
`chunk_size` |
`int`
The size of the chunks. |
`chunk_overlap` |
`int`
The overlap between chunks. |

## Classes

### FixedLengthChunking

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

## Methods

### RagFileChunkingConfig

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexStats -->

# Class IndexStats (1.135.0)

`IndexStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of the Index.

## Attributes |
|
|---|---|
Name |
Description |
`vectors_count` |
`int`
Output only. The number of dense vectors in the Index. |
`sparse_vectors_count` |
`int`
Output only. The number of sparse vectors in the Index. |
`shards_count` |
`int`
Output only. The number of shards in the Index. |

## Methods

### IndexStats

`IndexStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of the Index.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDataKey.CompositeKey -->

# Class CompositeKey (1.135.0)

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

## Attribute |
|
|---|---|
Name |
Description |
`parts` |
`MutableSequence[str]`
Parts to construct Entity ID. Should match with the same ID columns as defined in FeatureView in the same order. |

## Methods

### CompositeKey

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOperationMetadata -->

# Class UpdateFeatureOperationMetadata (1.135.0)

```
UpdateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Feature.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Feature Update. |

## Methods

### UpdateFeatureOperationMetadata

```
UpdateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictResponse -->

# Class DirectPredictResponse (1.135.0)

`DirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectPredict.

## Attributes |
|
|---|---|
Name |
Description |
`outputs` |
`MutableSequence[`
The prediction output. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### DirectPredictResponse

`DirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectPredict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.InlineSource -->

# Class InlineSource (1.135.0)

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

## Attribute |
|
|---|---|
Name |
Description |
`source_archive` |
`bytes`
Required. Input only. The application source code archive, provided as a compressed tarball (.tar.gz) file. |

## Methods

### InlineSource

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationQualityInput -->

# Class SummarizationQualityInput (1.135.0)

`SummarizationQualityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization quality score metric. |
`instance` |
Required. Summarization quality instance. |

## Methods

### SummarizationQualityInput

`SummarizationQualityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization quality metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest -->

# Class CreateFeatureRequest (1.135.0)

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`feature` |
Required. The Feature to create. |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within an EntityType/FeatureGroup.
|

## Methods

### CreateFeatureRequest

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringRelevanceResult -->

# Class QuestionAnsweringRelevanceResult (1.135.0)

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Relevance score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering relevance score. |
`confidence` |
`float`
Output only. Confidence for question answering relevance score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringRelevanceResult

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationHyperParameters -->

# Class DistillationHyperParameters (1.135.0)

`DistillationHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. This field is a member of `oneof` _ `_epoch_count` .
|
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. This field is a member of `oneof` _ `_learning_rate_multiplier` .
|
`adapter_size` |
Optional. Adapter size for distillation. |

## Methods

### DistillationHyperParameters

`DistillationHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometInstance -->

# Class CometInstance (1.135.0)

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

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
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### CometInstance

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool.GoogleSearch -->

# Class GoogleSearch (1.135.0)

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: ["amazon.com", "facebook.com"]. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest -->

# Class MutateDeployedModelRequest (1.135.0)

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - `min_replica_count` in either
DedicatedResources
or
AutomaticResources
- `max_replica_count` in either
DedicatedResources
or
AutomaticResources
- `required_replica_count` in
DedicatedResources
- autoscaling_metric_specs
- `disable_container_logging` (v1 only)
- `enable_container_logging` (v1beta1 only)
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### MutateDeployedModelRequest

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamDirectRawPredictResponse -->

# Class StreamDirectRawPredictResponse (1.135.0)

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### StreamDirectRawPredictResponse

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationSpec -->

# Class ExplanationSpec (1.135.0)

`ExplanationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of Model explanation.

## Attributes |
|
|---|---|
Name |
Description |
`parameters` |
Required. Parameters that configure explaining of the Model's predictions. |
`metadata` |
Optional. Metadata describing the Model's input and output for explanation. |

## Methods

### ExplanationSpec

`ExplanationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of Model explanation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest -->

# Class BatchCreateFeaturesRequest (1.135.0)

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each
child request message can be omitted. If `parent` is set
in a child request, then the value must match the `parent`
value in this request message.
|

## Methods

### BatchCreateFeaturesRequest

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelsPager -->

# Class ListModelsPager (1.134.0)

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModels`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelsPager

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictRequest -->

# Class StreamingRawPredictRequest (1.134.0)

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### StreamingRawPredictRequest

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.PredictionHandler -->

# Class PredictionHandler (1.134.0)

```
PredictionHandler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Default prediction handler for the prediction requests sent to the application.

## Methods

### PredictionHandler

```
PredictionHandler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Initializes a Handler instance.

Parameters |
|
|---|---|
Name |
Description |
`artifacts_uri` |
`str`
Required. The value of the environment variable AIP_STORAGE_URI. |
`predictor` |
`Type[Predictor]`
Optional. The Predictor class this handler uses to initiate predictor instance if given. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If predictor is None. |

### handle

`handle(request: starlette.requests.Request) -> starlette.responses.Response`


Handles a prediction request.

Parameter |
|
|---|---|
Name |
Description |
`request` |
`Request`
Required. The prediction request sent to the application. |

Exceptions |
|
|---|---|
Type |
Description |
`HTTPException` |
If any exception is thrown from predictor object. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNasJobRequest -->

# Class DeleteNasJobRequest (1.134.0)

`DeleteNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob resource to be deleted. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### DeleteNasJobRequest

`DeleteNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteNasJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.ModelConfig -->

# Class ModelConfig (1.134.0)

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for model selection.

## Attribute |
|
|---|---|
Name |
Description |
`feature_selection_preference` |
Required. Feature selection preference. |

## Classes

### FeatureSelectionPreference

`FeatureSelectionPreference(value)`


Options for feature selection preference.

## Methods

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for model selection.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchResults -->

# Class TrajectoryExactMatchResults (1.134.0)

`TrajectoryExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryExactMatch metric.

## Attribute |
|
|---|---|
Name |
Description |
`trajectory_exact_match_metric_values` |
`MutableSequence[`
Output only. TrajectoryExactMatch metric values. |

## Methods

### TrajectoryExactMatchResults

`TrajectoryExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryExactMatch metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecResponse.Recommendation.QuotaState -->

# Class QuotaState (1.134.0)

`QuotaState(value)`


The user accelerator quota state.

## Enums |
|
|---|---|
Name |
Description |
`QUOTA_STATE_UNSPECIFIED` |
Unspecified quota state. Quota information not available. |
`QUOTA_STATE_USER_HAS_QUOTA` |
User has enough accelerator quota for the machine type. |
`QUOTA_STATE_NO_USER_QUOTA` |
User does not have enough accelerator quota for the machine type. |

## Methods

### QuotaState

`QuotaState(value)`


The user accelerator quota state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest -->

# Class DeployRequest (1.134.0)

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
`publisher_model_name` |
`str`
The Model Garden model to deploy. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` .
This field is a member of `oneof` _ `artifacts` .
|
`hugging_face_model_id` |
`str`
The Hugging Face model to deploy. Format: Hugging Face model ID like `google/gemma-2-2b-it` .
This field is a member of `oneof` _ `artifacts` .
|
`destination` |
`str`
Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`model_config` |
Optional. The model config to use for the deployment. If not specified, the default model config will be used. |
`endpoint_config` |
Optional. The endpoint config to use for the deployment. If not specified, the default endpoint config will be used. |
`deploy_config` |
Optional. The deploy config to use for the deployment. If not specified, the default deploy config will be used. |

## Classes

### DeployConfig

`DeployConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The deploy config to use for the deployment.

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Methods

### DeployRequest

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardTimeSeriesRequest -->

# Class UpdateTensorboardTimeSeriesRequest (1.134.0)

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardTimeSeries resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries' `name` field is used
to identify the TensorboardTimeSeries to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### UpdateTensorboardTimeSeriesRequest

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs.ModelType -->

# Class ModelType (1.134.0)

A model to be used via prediction calls to uCAIP API. Expected to have a higher latency, but should also have a higher prediction quality than other models.

CLOUD_LOW_ACCURACY_1

A model to be used via prediction calls to uCAIP API. Expected to have a lower latency but relatively lower prediction quality.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataResponse -->

# Class GenerateSyntheticDataResponse (1.134.0)

```
GenerateSyntheticDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The response containing the generated data.

## Attribute |
|
|---|---|
Name |
Description |
`synthetic_examples` |
`MutableSequence[`
A list of generated synthetic examples. |

## Methods

### GenerateSyntheticDataResponse

```
GenerateSyntheticDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The response containing the generated data.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.ExplanationConfig.ExplanationBaseline.PredictionFormat -->

# Class PredictionFormat (1.134.0)

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

## Enums |
|
|---|---|
Name |
Description |
`PREDICTION_FORMAT_UNSPECIFIED` |
Should not be set. |
`JSONL` |
Predictions are in JSONL files. |
`BIGQUERY` |
Predictions are in BigQuery. |

## Methods

### PredictionFormat

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardSizeResponse -->

# Class ReadTensorboardSizeResponse (1.134.0)

`ReadTensorboardSizeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ReadTensorboardSize.

## Attribute |
|
|---|---|
Name |
Description |
`storage_size_byte` |
`int`
Payload storage size for the TensorBoard |

## Methods

### ReadTensorboardSizeResponse

`ReadTensorboardSizeResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ReadTensorboardSize.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighbors -->

# Class NearestNeighbors (1.134.0)

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

## Attribute |
|
|---|---|
Name |
Description |
`neighbors` |
`MutableSequence[`
All its neighbors. |

## Classes

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Methods

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping -->

# Class DatapointFieldMapping (1.134.0)

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.

## Attributes |
|
|---|---|
Name |
Description |
`id_column` |
`str`
Required. The column with unique identifiers for each data point. |
`embedding_column` |
`str`
Required. The column with the vector embeddings for each data point. |
`restricts` |
`MutableSequence[`
Optional. List of restricts for string values. |
`numeric_restricts` |
`MutableSequence[`
Optional. List of restricts for numeric values. |
`metadata_columns` |
`MutableSequence[str]`
Optional. List of columns containing metadata to be included in the index. |

## Classes

### NumericRestrict

`NumericRestrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on numeric values.

### Restrict

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.

## Methods

### DatapointFieldMapping

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.GoogleSearch -->

# Class GoogleSearch (1.134.0)

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: ["amazon.com", "facebook.com"]. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest -->

# Class MutateDeployedModelRequest (1.134.0)

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - `min_replica_count` in either
DedicatedResources
or
AutomaticResources
- `max_replica_count` in either
DedicatedResources
or
AutomaticResources
- `required_replica_count` in
DedicatedResources
- autoscaling_metric_specs
- `disable_container_logging` (v1 only)
- `enable_container_logging` (v1beta1 only)
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### MutateDeployedModelRequest

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest -->

# Class BatchCreateFeaturesRequest (1.134.0)

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each
child request message can be omitted. If `parent` is set
in a child request, then the value must match the `parent`
value in this request message.
|

## Methods

### BatchCreateFeaturesRequest

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsPager -->

# Class ListTrialsPager (1.134.0)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrialsPager

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsPager -->

# Class ListNasJobsPager (1.134.0)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasJobsPager

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileChunkingConfig -->

# Class RagFileChunkingConfig (1.134.0)

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`fixed_length_chunking` |
Specifies the fixed length chunking config. This field is a member of `oneof` _ `chunking_config` .
|
`chunk_size` |
`int`
The size of the chunks. |
`chunk_overlap` |
`int`
The overlap between chunks. |

## Classes

### FixedLengthChunking

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

## Methods

### RagFileChunkingConfig

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexStats -->

# Class IndexStats (1.134.0)

`IndexStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of the Index.

## Attributes |
|
|---|---|
Name |
Description |
`vectors_count` |
`int`
Output only. The number of dense vectors in the Index. |
`sparse_vectors_count` |
`int`
Output only. The number of sparse vectors in the Index. |
`shards_count` |
`int`
Output only. The number of shards in the Index. |

## Methods

### IndexStats

`IndexStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of the Index.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDataKey.CompositeKey -->

# Class CompositeKey (1.134.0)

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

## Attribute |
|
|---|---|
Name |
Description |
`parts` |
`MutableSequence[str]`
Parts to construct Entity ID. Should match with the same ID columns as defined in FeatureView in the same order. |

## Methods

### CompositeKey

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOperationMetadata -->

# Class UpdateFeatureOperationMetadata (1.134.0)

```
UpdateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Feature.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Feature Update. |

## Methods

### UpdateFeatureOperationMetadata

```
UpdateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictResponse -->

# Class DirectPredictResponse (1.134.0)

`DirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectPredict.

## Attributes |
|
|---|---|
Name |
Description |
`outputs` |
`MutableSequence[`
The prediction output. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### DirectPredictResponse

`DirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectPredict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.InlineSource -->

# Class InlineSource (1.134.0)

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

## Attribute |
|
|---|---|
Name |
Description |
`source_archive` |
`bytes`
Required. Input only. The application source code archive, provided as a compressed tarball (.tar.gz) file. |

## Methods

### InlineSource

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationQualityInput -->

# Class SummarizationQualityInput (1.134.0)

`SummarizationQualityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization quality score metric. |
`instance` |
Required. Summarization quality instance. |

## Methods

### SummarizationQualityInput

`SummarizationQualityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization quality metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest -->

# Class CreateFeatureRequest (1.134.0)

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`feature` |
Required. The Feature to create. |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within an EntityType/FeatureGroup.
|

## Methods

### CreateFeatureRequest

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringRelevanceResult -->

# Class QuestionAnsweringRelevanceResult (1.134.0)

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Relevance score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering relevance score. |
`confidence` |
`float`
Output only. Confidence for question answering relevance score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringRelevanceResult

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationHyperParameters -->

# Class DistillationHyperParameters (1.134.0)

`DistillationHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. This field is a member of `oneof` _ `_epoch_count` .
|
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. This field is a member of `oneof` _ `_learning_rate_multiplier` .
|
`adapter_size` |
Optional. Adapter size for distillation. |

## Methods

### DistillationHyperParameters

`DistillationHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometInstance -->

# Class CometInstance (1.134.0)

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

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
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### CometInstance

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool.GoogleSearch -->

# Class GoogleSearch (1.134.0)

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: ["amazon.com", "facebook.com"]. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest -->

# Class MutateDeployedModelRequest (1.134.0)

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - `min_replica_count` in either
DedicatedResources
or
AutomaticResources
- `max_replica_count` in either
DedicatedResources
or
AutomaticResources
- `required_replica_count` in
DedicatedResources
- autoscaling_metric_specs
- `disable_container_logging` (v1 only)
- `enable_container_logging` (v1beta1 only)
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### MutateDeployedModelRequest

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamDirectRawPredictResponse -->

# Class StreamDirectRawPredictResponse (1.134.0)

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### StreamDirectRawPredictResponse

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationSpec -->

# Class ExplanationSpec (1.134.0)

`ExplanationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of Model explanation.

## Attributes |
|
|---|---|
Name |
Description |
`parameters` |
Required. Parameters that configure explaining of the Model's predictions. |
`metadata` |
Optional. Metadata describing the Model's input and output for explanation. |

## Methods

### ExplanationSpec

`ExplanationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of Model explanation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest -->

# Class BatchCreateFeaturesRequest (1.134.0)

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each
child request message can be omitted. If `parent` is set
in a child request, then the value must match the `parent`
value in this request message.
|

## Methods

### BatchCreateFeaturesRequest

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient -->

# Class ModelGardenServiceAsyncClient (1.134.0)

```
ModelGardenServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### ModelGardenServiceAsyncClient

```
ModelGardenServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model garden service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelGardenServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_accept_publisher_model_eula():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AcceptPublisherModelEulaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceptPublisherModelEulaRequest.html)(
parent="parent_value",
publisher_model="publisher_model_value",
)
# Make the request
response = await client.[accept_publisher_model_eula](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_accept_publisher_model_eula)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelGardenService.AcceptPublisherModelEula. |
`parent` |
Required. The project requesting access for named model. The format is |
`publisher_model` |
Required. The name of the PublisherModel resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_check_publisher_model_eula_acceptance():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CheckPublisherModelEulaAcceptanceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckPublisherModelEulaAcceptanceRequest.html)(
parent="parent_value",
publisher_model="publisher_model_value",
)
# Make the request
response = await client.[check_publisher_model_eula_acceptance](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_check_publisher_model_eula_acceptance)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ModelGardenService.CheckPublisherModelEula][]. |
`parent` |
Required. The project requesting access for named model. The format is |
`publisher_model` |
Required. The name of the PublisherModel resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_deploy():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeployRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.html)(
publisher_model_name="publisher_model_name_value",
destination="destination_value",
)
# Make the request
operation = client.[deploy](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_deploy)(request=request)
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
The request object. Request message for ModelGardenService.Deploy. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_deploy_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeployPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelRequest.html)(
model="model_value",
destination="destination_value",
)
# Make the request
operation = client.[deploy_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_deploy_publisher_model)(request=request)
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
The request object. Request message for ModelGardenService.DeployPublisherModel. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_export_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1beta1.[GcsDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsDestination.html)()
destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ExportPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelRequest.html)(
name="name_value",
destination=destination,
parent="parent_value",
)
# Make the request
operation = client.[export_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_export_publisher_model)(request=request)
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
The request object. Request message for ModelGardenService.ExportPublisherModel. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ModelGardenServiceAsyncClient` |
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
`ModelGardenServiceAsyncClient` |
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
`ModelGardenServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPublisherModelRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_get_publisher_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelGardenService.GetPublisherModel |
`name` |
Required. The name of the PublisherModel resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsAsyncPager
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
async def sample_list_publisher_models():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPublisherModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_publisher_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceAsyncClient_list_publisher_models)(request=request)
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
The request object. Request message for ModelGardenService.ListPublisherModels. |
`parent` |
Required. The name of the Publisher from which to list the PublisherModels. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient -->

# Class SessionServiceAsyncClient (1.134.0)

```
SessionServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### SessionServiceAsyncClient

```
SessionServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the session service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the SessionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_append_event():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
event = aiplatform_v1beta1.[SessionEvent](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SessionEvent.html)()
event.author = "author_value"
event.invocation_id = "invocation_id_value"
request = aiplatform_v1beta1.[AppendEventRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventRequest.html)(
name="name_value",
event=event,
)
# Make the request
response = await client.[append_event](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_append_event)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for SessionService.AppendEvent. |
`name` |
Required. The resource name of the session to append event to. Format: |
`event` |
Required. The event to append to the session. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
session = aiplatform_v1beta1.[Session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session.html)()
session.user_id = "user_id_value"
request = aiplatform_v1beta1.[CreateSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSessionRequest.html)(
parent="parent_value",
session=session,
)
# Make the request
operation = client.[create_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_create_session)(request=request)
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
The request object. Request message for SessionService.CreateSession. |
`parent` |
Required. The resource name of the location to create the session in. Format: |
`session` |
`Session`
Required. The session to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSessionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_delete_session)(request=request)
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
The request object. Request message for SessionService.DeleteSession. |
`name` |
Required. The resource name of the session. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`SessionServiceAsyncClient` |
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
`SessionServiceAsyncClient` |
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
`SessionServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSessionRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_get_session)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for SessionService.GetSession. |
`name` |
Required. The resource name of the session. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsAsyncPager
)
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
async def sample_list_events():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEventsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_events](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_list_events)(request=request)
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
The request object. Request message for SessionService.ListEvents. |
`parent` |
Required. The resource name of the session to list events from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsAsyncPager
)
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
async def sample_list_sessions():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSessionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_sessions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_list_sessions)(request=request)
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
The request object. Request message for SessionService.ListSessions. |
`parent` |
Required. The resource name of the location to list sessions from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_update_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html)()
# Initialize request argument(s)
session = aiplatform_v1beta1.[Session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session.html)()
session.user_id = "user_id_value"
request = aiplatform_v1beta1.[UpdateSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSessionRequest.html)(
session=session,
)
# Make the request
response = await client.[update_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceAsyncClient_update_session)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for SessionService.UpdateSession. |
`session` |
`Session`
Required. The session to update. Format: |
`update_mask` |
Optional. Field mask is used to control which fields get updated. If the mask is not present, all fields will be updated. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient -->

# Class MemoryBankServiceAsyncClient (1.134.0)

```
MemoryBankServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### MemoryBankServiceAsyncClient

```
MemoryBankServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the memory bank service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the MemoryBankServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
memory = aiplatform_v1beta1.[Memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.html)()
memory.fact = "fact_value"
request = aiplatform_v1beta1.[CreateMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryRequest.html)(
parent="parent_value",
memory=memory,
)
# Make the request
operation = client.[create_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_create_memory)(request=request)
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
The request object. Request message for MemoryBankService.CreateMemory. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMemoryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_delete_memory)(request=request)
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
The request object. Request message for MemoryBankService.DeleteMemory. |
`name` |
Required. The resource name of the Memory to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`MemoryBankServiceAsyncClient` |
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
`MemoryBankServiceAsyncClient` |
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
`MemoryBankServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_generate_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
vertex_session_source = aiplatform_v1beta1.[VertexSessionSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.VertexSessionSource.html)()
vertex_session_source.session = "session_value"
request = aiplatform_v1beta1.[GenerateMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.html)(
vertex_session_source=vertex_session_source,
parent="parent_value",
)
# Make the request
operation = client.[generate_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_generate_memories)(request=request)
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
The request object. Request message for MemoryBankService.GenerateMemories. |
`parent` |
Required. The resource name of the ReasoningEngine to generate memories for. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMemoryRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_get_memory)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MemoryBankService.GetMemory. |
`name` |
Required. The resource name of the Memory. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesAsyncPager
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
async def sample_list_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_list_memories)(request=request)
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
The request object. Request message for MemoryBankService.ListMemories. |
`parent` |
Required. The resource name of the ReasoningEngine to list the Memories under. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_retrieve_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
similarity_search_params = aiplatform_v1beta1.[SimilaritySearchParams](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.SimilaritySearchParams.html)()
similarity_search_params.search_query = "search_query_value"
request = aiplatform_v1beta1.[RetrieveMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.html)(
similarity_search_params=similarity_search_params,
parent="parent_value",
)
# Make the request
response = await client.[retrieve_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_retrieve_memories)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MemoryBankService.RetrieveMemories. |
`parent` |
Required. The resource name of the ReasoningEngine to retrieve memories from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_update_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html)()
# Initialize request argument(s)
memory = aiplatform_v1beta1.[Memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.html)()
memory.fact = "fact_value"
request = aiplatform_v1beta1.[UpdateMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryRequest.html)(
memory=memory,
)
# Make the request
operation = client.[update_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceAsyncClient_update_memory)(request=request)
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
The request object. Request message for MemoryBankService.UpdateMemory. |
`memory` |
Required. The Memory which replaces the resource on the server. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesPager -->

# Class ListIndexesPager (1.134.0)

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse) object, and
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

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexesPager

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.BigQuery.TimeSeries -->

# Class TimeSeries (1.134.0)

`TimeSeries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`timestamp_column` |
`str`
Optional. Column hosting timestamp values for a time-series source. Will be used to determine the latest `feature_values` for each entity. Optional. If not
provided, column named `feature_timestamp` of type
`TIMESTAMP` will be used.
|

## Methods

### TimeSeries

`TimeSeries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQuerySource -->

# Class BigQuerySource (1.134.0)

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the input content.

## Attribute |
|
|---|---|
Name |
Description |
`input_uri` |
`str`
Required. BigQuery URI to a table, up to 2000 characters long. Accepted forms: - BigQuery path. For example: `bq://projectId.bqDatasetId.bqTableId` .
|

## Methods

### BigQuerySource

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the input content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest -->

# Class CreateFeatureRequest (1.134.0)

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`feature` |
Required. The Feature to create. |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within an EntityType/FeatureGroup.
|

## Methods

### CreateFeatureRequest

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation -->

# Class Transformation (1.134.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule -->

# Class Schedule (1.134.0)

`Schedule(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

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
`cron` |
`str`
Cron schedule (https://en.wikipedia.org/wiki/Cron) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*". This field is a member of `oneof` _ `time_specification` .
|
`create_pipeline_job_request` |
Request for PipelineService.CreatePipelineJob. CreatePipelineJobRequest.parent field is required (format: projects/{project}/locations/{location}). This field is a member of `oneof` _ `request` .
|
`create_notebook_execution_job_request` |
Request for NotebookService.CreateNotebookExecutionJob. This field is a member of `oneof` _ `request` .
|
`name` |
`str`
Immutable. The resource name of the Schedule. |
`display_name` |
`str`
Required. User provided name of the Schedule. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp after which the first run can be scheduled. Default to Schedule create time if not specified. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp after which no new runs can be scheduled. If specified, The schedule will be completed when either end_time is reached or when scheduled_run_count >= max_run_count. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified. |
`max_run_count` |
`int`
Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count >= max_run_count or when end_time is reached. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified. |
`started_run_count` |
`int`
Output only. The number of runs started by this schedule. |
`state` |
Output only. The state of this Schedule. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was updated. |
`next_run_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule should schedule the next run. Having a next_run_time in the past means the runs are being started behind schedule. |
`last_pause_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was last paused. Unset if never paused. |
`last_resume_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was last resumed. Unset if never resumed from pause. |
`max_concurrent_run_count` |
`int`
Required. Maximum number of runs that can be started concurrently for this Schedule. This is the limit for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). |
`allow_queueing` |
`bool`
Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. If set to true, new runs will be queued instead of skipped. Default to false. |
`catch_up` |
`bool`
Output only. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. Default to false. |
`last_scheduled_run_response` |
Output only. Response of the last scheduled run. This is the response for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). Unset if no run has been scheduled yet. |

## Classes

### RunResponse

`RunResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Status of a scheduled run.

### State

`State(value)`


Possible state of the schedule.

## Methods

### Schedule

`Schedule(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.Documentation -->

# Class Documentation (1.134.0)

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

## Attributes |
|
|---|---|
Name |
Description |
`title` |
`str`
Required. E.g., OVERVIEW, USE CASES, DOCUMENTATION, SDK & SAMPLES, JAVA, NODE.JS, etc.. |
`content` |
`str`
Required. Content of this piece of document (in Markdown format). |

## Methods

### Documentation

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Artifact.State -->

# Class State (1.134.0)

`State(value)`


Describes the state of the Artifact.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified state for the Artifact. |
`PENDING` |
A state used by systems like Vertex AI Pipelines to indicate that the underlying data item represented by this Artifact is being created. |
`LIVE` |
A state indicating that the Artifact should exist, unless something external to the system deletes it. |

## Methods

### State

`State(value)`


Describes the state of the Artifact.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceResult -->

# Class QuestionAnsweringRelevanceResult (1.134.0)

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Relevance score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering relevance score. |
`confidence` |
`float`
Output only. Confidence for question answering relevance score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringRelevanceResult

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardExperiment -->

# Class TensorboardExperiment (1.134.0)

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the TensorboardExperiment. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`display_name` |
`str`
User provided name of this TensorboardExperiment. |
`description` |
`str`
Description of this TensorboardExperiment. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your TensorboardExperiment. Label keys and values cannot be longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with `aiplatform.googleapis.com/` and are immutable. The
following system labels exist for each Dataset:
- `aiplatform.googleapis.com/dataset_metadata_schema` :
output only. Its value is the
[metadata_schema's][google.cloud.aiplatform.v1.Dataset.metadata_schema_uri]
title.
|
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`source` |
`str`
Immutable. Source of the TensorboardExperiment. Example: a custom training job. |

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

### TensorboardExperiment

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.Maps.PlaceAnswerSources.ReviewSnippet -->

# Class ReviewSnippet (1.134.0)

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Attributes |
|
|---|---|
Name |
Description |
`review_id` |
`str`
Id of the review referencing the place. |
`google_maps_uri` |
`str`
A link to show the review on Google Maps. |
`title` |
`str`
Title of the review. |

## Methods

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryOperationMetadata -->

# Class UpdateMemoryOperationMetadata (1.134.0)

```
UpdateMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.UpdateMemory operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateMemoryOperationMetadata

```
UpdateMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.UpdateMemory operation.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMemoryOperationMetadata -->

# Class DeleteMemoryOperationMetadata (1.134.0)

```
DeleteMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.DeleteMemory operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### DeleteMemoryOperationMetadata

```
DeleteMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.DeleteMemory operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service -->

# Package llm_utility_service (1.134.0)

API documentation for `aiplatform_v1.services.llm_utility_service`

package.

## Classes

[LlmUtilityServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceAsyncClient)

Service for LLM related utility functions.

[LlmUtilityServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceClient)

Service for LLM related utility functions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationInputs.ModelType -->

# Class ModelType (1.134.0)

A model to be used via prediction calls to uCAIP API. Expected to have a higher latency, but should also have a higher prediction quality than other models.

CLOUD_LOW_ACCURACY_1

A model to be used via prediction calls to uCAIP API. Expected to have a lower latency but relatively lower prediction quality.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometInstance -->

# Class CometInstance (1.134.0)

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

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
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### CometInstance

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTuningJobRequest -->

# Class GetTuningJobRequest (1.134.0)

`GetTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.GetTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TuningJob resource. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|

## Methods

### GetTuningJobRequest

`GetTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.GetTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GoogleSearchRetrieval -->

# Class GoogleSearchRetrieval (1.134.0)

`GoogleSearchRetrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public web data for grounding, powered by Google.

## Attribute |
|
|---|---|
Name |
Description |
`dynamic_retrieval_config` |
Specifies the dynamic retrieval configuration for the given source. |

## Methods

### GoogleSearchRetrieval

`GoogleSearchRetrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public web data for grounding, powered by Google.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualityResult -->

# Class PairwiseQuestionAnsweringQualityResult (1.134.0)

```
PairwiseQuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise question answering prediction choice. |
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseQuestionAnsweringQualityResult

```
PairwiseQuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.Parent -->

# Class Parent (1.134.0)

`Parent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The information about the parent of a model.

## Attributes |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The display name of the parent. E.g., LaMDA, T5, Vision API, Natural Language API. |
`reference` |
Optional. The Google Cloud resource name or the URI reference. |

## Methods

### Parent

`Parent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The information about the parent of a model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryOperationMetadata -->

# Class CreateMemoryOperationMetadata (1.134.0)

```
CreateMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.CreateMemory operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### CreateMemoryOperationMetadata

```
CreateMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.CreateMemory operation.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagChunk.PageSpan -->

# Class PageSpan (1.134.0)

`PageSpan(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents where the chunk starts and ends in the document.

## Attributes |
|
|---|---|
Name |
Description |
`first_page` |
`int`
Page where chunk starts in the document. Inclusive. 1-indexed. |
`last_page` |
`int`
Page where chunk ends in the document. Inclusive. 1-indexed. |

## Methods

### PageSpan

`PageSpan(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents where the chunk starts and ends in the document.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexOperationMetadata -->

# Class ImportIndexOperationMetadata (1.134.0)

```
ImportIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.ImportIndex.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### ImportIndexOperationMetadata

```
ImportIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.ImportIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation -->

# Class Transformation (1.134.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesPager -->

# Class ListStudiesPager (1.134.0)

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__iter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__iter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListStudiesPager

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringConfig -->

# Class ModelMonitoringConfig (1.134.0)

`ModelMonitoringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model monitoring configuration used for Batch Prediction Job.

## Attributes |
|
|---|---|
Name |
Description |
`objective_configs` |
`MutableSequence[`
Model monitoring objective config. |
`alert_config` |
Model monitoring alert config. |
`analysis_instance_schema_uri` |
`str`
YAML schema file uri in Cloud Storage describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`stats_anomalies_base_directory` |
A Google Cloud Storage location for batch prediction model monitoring to dump statistics and anomalies. If not provided, a folder will be created in customer project to hold statistics and anomalies. |

## Methods

### ModelMonitoringConfig

`ModelMonitoringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model monitoring configuration used for Batch Prediction Job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexStats -->

# Class IndexStats (1.134.0)

`IndexStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of the Index.

## Attributes |
|
|---|---|
Name |
Description |
`vectors_count` |
`int`
Output only. The number of dense vectors in the Index. |
`sparse_vectors_count` |
`int`
Output only. The number of sparse vectors in the Index. |
`shards_count` |
`int`
Output only. The number of shards in the Index. |

## Methods

### IndexStats

`IndexStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of the Index.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UrlMetadata -->

# Class UrlMetadata (1.134.0)

`UrlMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Context of the a single url retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`retrieved_url` |
`str`
Retrieved url by the tool. |
`url_retrieval_status` |
Status of the url retrieval. |

## Classes

### UrlRetrievalStatus

`UrlRetrievalStatus(value)`


Status of the url retrieval.

## Methods

### UrlMetadata

`UrlMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Context of the a single url retrieval.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient -->

# Class DeploymentResourcePoolServiceAsyncClient (1.134.0)

```
DeploymentResourcePoolServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### DeploymentResourcePoolServiceAsyncClient

```
DeploymentResourcePoolServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the deployment resource pool service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the DeploymentResourcePoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_deployment_resource_pool

```
create_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.CreateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool.DeploymentResourcePool
] = None,
deployment_resource_pool_id: typing.Optional[str] = None,
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


Create a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1beta1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[CreateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolRequest.html)(
parent="parent_value",
deployment_resource_pool=deployment_resource_pool,
deployment_resource_pool_id="deployment_resource_pool_id_value",
)
# Make the request
operation = client.[create_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_create_deployment_resource_pool)(request=request)
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
The request object. Request message for CreateDeploymentResourcePool method. |
`parent` |
Required. The parent location resource where this DeploymentResourcePool will be created. Format: |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. This corresponds to the |
`deployment_resource_pool_id` |
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_deployment_resource_pool

```
delete_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.DeleteDeploymentResourcePoolRequest,
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


Delete a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_delete_deployment_resource_pool)(request=request)
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
The request object. Request message for DeleteDeploymentResourcePool method. |
`name` |
Required. The name of the DeploymentResourcePool to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`DeploymentResourcePoolServiceAsyncClient` |
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
`DeploymentResourcePoolServiceAsyncClient` |
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
`DeploymentResourcePoolServiceAsyncClient` |
The constructed client. |

### get_deployment_resource_pool

```
get_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.GetDeploymentResourcePoolRequest,
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool.DeploymentResourcePool
)
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
from google.cloud import aiplatform_v1beta1
async def sample_get_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_get_deployment_resource_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GetDeploymentResourcePool method. |
`name` |
Required. The name of the DeploymentResourcePool to retrieve. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport
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

### list_deployment_resource_pools

```
list_deployment_resource_pools(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
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
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_deployment_resource_pools():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDeploymentResourcePoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_deployment_resource_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_list_deployment_resource_pools)(request=request)
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
The request object. Request message for ListDeploymentResourcePools method. |
`parent` |
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_query_deployed_models():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[QueryDeployedModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsRequest.html)(
deployment_resource_pool="deployment_resource_pool_value",
)
# Make the request
page_result = client.[query_deployed_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_query_deployed_models)(request=request)
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
The request object. Request message for QueryDeployedModels method. |
`deployment_resource_pool` |
Required. The name of the target DeploymentResourcePool to query. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### update_deployment_resource_pool

```
update_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.UpdateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool.DeploymentResourcePool
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


Update a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_deployment_resource_pool():
# Create a client
client = aiplatform_v1beta1.
```[DeploymentResourcePoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1beta1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[UpdateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolRequest.html)(
deployment_resource_pool=deployment_resource_pool,
)
# Make the request
operation = client.[update_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceAsyncClient_update_deployment_resource_pool)(request=request)
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
The request object. Request message for UpdateDeploymentResourcePool method. |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to update. The DeploymentResourcePool's |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchInstance -->

# Class TrajectoryExactMatchInstance (1.134.0)

```
TrajectoryExactMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryExactMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|
`reference_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for reference tool call trajectory. This field is a member of `oneof` _ `_reference_trajectory` .
|

## Methods

### TrajectoryExactMatchInstance

```
TrajectoryExactMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryExactMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_garden_service -->

# Package model_garden_service (1.134.0)

API documentation for `aiplatform_v1.services.model_garden_service`

package.

## Classes

[ModelGardenServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_garden_service.ModelGardenServiceAsyncClient)

The interface of Model Garden Service.

[ModelGardenServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_garden_service.ModelGardenServiceClient)

The interface of Model Garden Service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagCorpusRequest -->

# Class GetRagCorpusRequest (1.134.0)

`GetRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagCorpus

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagCorpus resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|

## Methods

### GetRagCorpusRequest

`GetRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagCorpus

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardExperiment -->

# Class TensorboardExperiment (1.134.0)

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the TensorboardExperiment. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`display_name` |
`str`
User provided name of this TensorboardExperiment. |
`description` |
`str`
Description of this TensorboardExperiment. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardExperiment was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your TensorboardExperiment. Label keys and values cannot be longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with `aiplatform.googleapis.com/` and are immutable. The
following system labels exist for each Dataset:
- `aiplatform.googleapis.com/dataset_metadata_schema` :
output only. Its value is the
[metadata_schema's][google.cloud.aiplatform.v1beta1.Dataset.metadata_schema_uri]
title.
|
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`source` |
`str`
Immutable. Source of the TensorboardExperiment. Example: a custom training job. |

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

### TensorboardExperiment

`TensorboardExperiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDatasetRequest -->

# Class DeleteDatasetRequest (1.134.0)

`DeleteDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDataset.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|

## Methods

### DeleteDatasetRequest

`DeleteDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.AutoRoutingMode.ModelRoutingPreference -->

# Class ModelRoutingPreference (1.134.0)

`ModelRoutingPreference(value)`


The model routing preference.

## Enums |
|
|---|---|
Name |
Description |
`UNKNOWN` |
Unspecified model routing preference. |
`PRIORITIZE_QUALITY` |
Prefer higher quality over low cost. |
`BALANCED` |
Balanced model routing preference. |
`PRIORITIZE_COST` |
Prefer lower cost over higher quality. |

## Methods

### ModelRoutingPreference

`ModelRoutingPreference(value)`


The model routing preference.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityResult -->

# Class PairwiseQuestionAnsweringQualityResult (1.134.0)

```
PairwiseQuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise question answering prediction choice. |
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseQuestionAnsweringQualityResult

```
PairwiseQuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeaturestoreRequest -->

# Class UpdateFeaturestoreRequest (1.134.0)

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`featurestore` |
Required. The Featurestore's `name` field is used to
identify the Featurestore to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `online_serving_config.fixed_node_count`
- `online_serving_config.scaling`
- `online_storage_ttl_days`
|

## Methods

### UpdateFeaturestoreRequest

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service -->

# Package evaluation_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.evaluation_service`

package.

## Classes

[EvaluationServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient)

Vertex AI Online Evaluation Service.

[EvaluationServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient)

Vertex AI Online Evaluation Service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityInput -->

# Class SummarizationQualityInput (1.134.0)

`SummarizationQualityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization quality score metric. |
`instance` |
Required. Summarization quality instance. |

## Methods

### SummarizationQualityInput

`SummarizationQualityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization quality metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookSoftwareConfig -->

# Class NotebookSoftwareConfig (1.134.0)

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`colab_image` |
Optional. Google-managed NotebookRuntime colab image. This field is a member of `oneof` _ `runtime_image` .
|
`env` |
`MutableSequence[`
Optional. Environment variables to be passed to the container. Maximum limit is 100. |
`post_startup_script_config` |
Optional. Post startup script config. |

## Methods

### NotebookSoftwareConfig

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectRawPredictResponse -->

# Class StreamDirectRawPredictResponse (1.134.0)

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### StreamDirectRawPredictResponse

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail.ProcessedDataset -->

# Class ProcessedDataset (1.134.0)

`ProcessedDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Processed dataset information.

## Attributes |
|
|---|---|
Name |
Description |
`location` |
`str`
Actual data location of the processed dataset. |
`time_range` |
`google.type.interval_pb2.Interval`
Dataset time range information if any. |

## Methods

### ProcessedDataset

`ProcessedDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Processed dataset information.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.Documentation -->

# Class Documentation (1.134.0)

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

## Attributes |
|
|---|---|
Name |
Description |
`title` |
`str`
Required. E.g., OVERVIEW, USE CASES, DOCUMENTATION, SDK & SAMPLES, JAVA, NODE.JS, etc.. |
`content` |
`str`
Required. Content of this piece of document (in Markdown format). |

## Methods

### Documentation

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UsageMetadata.TrafficType -->

# Class TrafficType (1.134.0)

`TrafficType(value)`


The type of traffic that this request was processed with, indicating which quota gets consumed.

## Enums |
|
|---|---|
Name |
Description |
`TRAFFIC_TYPE_UNSPECIFIED` |
Unspecified request traffic type. |
`ON_DEMAND` |
Type for Pay-As-You-Go traffic. |
`PROVISIONED_THROUGHPUT` |
Type for Provisioned Throughput traffic. |

## Methods

### TrafficType

`TrafficType(value)`


The type of traffic that this request was processed with, indicating which quota gets consumed.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Claim -->

# Class Claim (1.134.0)

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Index in the input text where the claim starts (inclusive). This field is a member of `oneof` _ `_start_index` .
|
`end_index` |
`int`
Index in the input text where the claim ends (exclusive). This field is a member of `oneof` _ `_end_index` .
|
`fact_indexes` |
`MutableSequence[int]`
Indexes of the facts supporting this claim. |
`score` |
`float`
Confidence score of this corroboration. This field is a member of `oneof` _ `_score` .
|

## Methods

### Claim

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk.Maps.PlaceAnswerSources.ReviewSnippet -->

# Class ReviewSnippet (1.134.0)

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Attributes |
|
|---|---|
Name |
Description |
`review_id` |
`str`
Id of the review referencing the place. |
`google_maps_uri` |
`str`
A link to show the review on Google Maps. |
`title` |
`str`
Title of the review. |

## Methods

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetRequest -->

# Class GetDatasetRequest (1.134.0)

`GetDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDataset.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetDatasetRequest

`GetDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDataset.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.Maps.PlaceAnswerSources -->

# Class PlaceAnswerSources (1.134.0)

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`review_snippets` |
`MutableSequence[`
Snippets of reviews that are used to generate the answer. |

## Classes

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Methods

### PlaceAnswerSources

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleSearchRetrieval -->

# Class GoogleSearchRetrieval (1.134.0)

`GoogleSearchRetrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public web data for grounding, powered by Google.

## Attribute |
|
|---|---|
Name |
Description |
`dynamic_retrieval_config` |
Specifies the dynamic retrieval configuration for the given source. |

## Methods

### GoogleSearchRetrieval

`GoogleSearchRetrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public web data for grounding, powered by Google.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelsPager -->

# Class ListModelsPager (1.134.0)

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModels`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelsPager

```
ListModelsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesRequest -->

# Class SearchExamplesRequest (1.134.0)

`SearchExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.SearchExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`stored_contents_example_parameters` |
The parameters of StoredContentsExamples to be searched. This field is a member of `oneof` _ `parameters` .
|
`example_store` |
`str`
Required. The name of the ExampleStore resource that examples are retrieved from. Format: `projects/{project}/locations/{location}/exampleStores/{example_store}`
|
`top_k` |
`int`
Optional. The number of similar examples to return. |

## Methods

### SearchExamplesRequest

`SearchExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.SearchExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreRequest -->

# Class UpdateFeaturestoreRequest (1.134.0)

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`featurestore` |
Required. The Featurestore's `name` field is used to
identify the Featurestore to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `online_serving_config.fixed_node_count`
- `online_serving_config.scaling`
- `online_storage_ttl_days`
|

## Methods

### UpdateFeaturestoreRequest

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTuningJobRequest -->

# Class GetTuningJobRequest (1.134.0)

`GetTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.GetTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TuningJob resource. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|

## Methods

### GetTuningJobRequest

`GetTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.GetTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelCustomJobRequest -->

# Class CancelCustomJobRequest (1.134.0)

`CancelCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob to cancel. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### CancelCustomJobRequest

`CancelCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelCustomJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagChunk.PageSpan -->

# Class PageSpan (1.134.0)

`PageSpan(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents where the chunk starts and ends in the document.

## Attributes |
|
|---|---|
Name |
Description |
`first_page` |
`int`
Page where chunk starts in the document. Inclusive. 1-indexed. |
`last_page` |
`int`
Page where chunk ends in the document. Inclusive. 1-indexed. |

## Methods

### PageSpan

`PageSpan(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents where the chunk starts and ends in the document.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagFileRequest -->

# Class GetRagFileRequest (1.134.0)

`GetRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagFile

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagFile resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file}`
|

## Methods

### GetRagFileRequest

`GetRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagFile

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookSoftwareConfig -->

# Class NotebookSoftwareConfig (1.134.0)

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`colab_image` |
Optional. Google-managed NotebookRuntime colab image. This field is a member of `oneof` _ `runtime_image` .
|
`env` |
`MutableSequence[`
Optional. Environment variables to be passed to the container. Maximum limit is 100. |
`post_startup_script_config` |
Optional. Post-startup script config. |

## Methods

### NotebookSoftwareConfig

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxInstance -->

# Class MetricxInstance (1.134.0)

`MetricxInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

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
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### MetricxInstance

`MetricxInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlMetadata -->

# Class UrlMetadata (1.134.0)

`UrlMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Context of the a single url retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`retrieved_url` |
`str`
Retrieved url by the tool. |
`url_retrieval_status` |
Status of the url retrieval. |

## Classes

### UrlRetrievalStatus

`UrlRetrievalStatus(value)`


Status of the url retrieval.

## Methods

### UrlMetadata

`UrlMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Context of the a single url retrieval.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedIndexResponse -->

# Class MutateDeployedIndexResponse (1.134.0)

`MutateDeployedIndexResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.MutateDeployedIndex.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_index` |
The DeployedIndex that had been updated in the IndexEndpoint. |

## Methods

### MutateDeployedIndexResponse

`MutateDeployedIndexResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.MutateDeployedIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Claim -->

# Class Claim (1.134.0)

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Index in the input text where the claim starts (inclusive). This field is a member of `oneof` _ `_start_index` .
|
`end_index` |
`int`
Index in the input text where the claim ends (exclusive). This field is a member of `oneof` _ `_end_index` .
|
`fact_indexes` |
`MutableSequence[int]`
Indexes of the facts supporting this claim. |
`score` |
`float`
Confidence score of this corroboration. This field is a member of `oneof` _ `_score` .
|

## Methods

### Claim

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.AutoRoutingMode -->

# Class AutoRoutingMode (1.134.0)

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_routing_preference` |
The model routing preference. This field is a member of `oneof` _ `_model_routing_preference` .
|

## Classes

### ModelRoutingPreference

`ModelRoutingPreference(value)`


The model routing preference.

## Methods

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntimeType -->

# Class NotebookRuntimeType (1.134.0)

`NotebookRuntimeType(value)`


Represents a notebook runtime type.

## Enums |
|
|---|---|
Name |
Description |
`NOTEBOOK_RUNTIME_TYPE_UNSPECIFIED` |
Unspecified notebook runtime type, NotebookRuntimeType will default to USER_DEFINED. |
`USER_DEFINED` |
runtime or template with coustomized configurations from user. |
`ONE_CLICK` |
runtime or template with system defined configurations. |

## Methods

### NotebookRuntimeType

`NotebookRuntimeType(value)`


Represents a notebook runtime type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagCorpusRequest -->

# Class GetRagCorpusRequest (1.134.0)

`GetRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagCorpus

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagCorpus resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|

## Methods

### GetRagCorpusRequest

`GetRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagCorpus

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Context -->

# Class Context (1.134.0)

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general context.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. The resource name of the Context. |
`display_name` |
`str`
User provided display name of the Context. May be up to 128 Unicode characters. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Contexts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Context was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Context was last updated. |
`parent_contexts` |
`MutableSequence[str]`
Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parent_contexts. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Context. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Context |

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

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general context.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsPager -->

# Class ListDatasetsPager (1.134.0)

```
ListDatasetsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse,
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


A pager for iterating through `list_datasets`

requests.

This class thinly wraps an initial
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse) object, and
provides an `__iter__`

method to iterate through its
`datasets`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDatasets`

requests and continue to iterate
through the `datasets`

field on the
corresponding responses.

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetsPager

```
ListDatasetsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsPager -->

# Class ListTrialsPager (1.134.0)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrialsPager

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient -->

# Class IndexServiceClient (1.134.0)

```
IndexServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Index resources.

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
`IndexServiceTransport` |
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

### IndexServiceClient

```
IndexServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexServiceTransport,Callable[..., IndexServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index

```
create_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.CreateIndexRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
index: typing.Optional[google.cloud.aiplatform_v1beta1.types.index.Index] = None,
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


Creates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
index = aiplatform_v1beta1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexRequest.html)(
parent="parent_value",
index=index,
)
# Make the request
operation = client.[create_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_create_index)(request=request)
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
The request object. Request message for IndexService.CreateIndex. |
`parent` |
`str`
Required. The resource name of the Location to create the Index in. Format: |
`index` |
Required. The Index to create. This corresponds to the |
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

### delete_index

```
delete_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.DeleteIndexRequest, dict
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


Deletes an Index. An Index can only be deleted when all its xref_DeployedIndexes had been undeployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_delete_index)(request=request)
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
The request object. Request message for IndexService.DeleteIndex. |
`name` |
`str`
Required. The name of the Index resource to be deleted. Format: |
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
`IndexServiceClient` |
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
`IndexServiceClient` |
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
`IndexServiceClient` |
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

### get_index

```
get_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.GetIndexRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.types.index.Index
```


Gets an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_get_index)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexService.GetIndex |
`name` |
`str`
Required. The name of the Index resource. Format: |
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
A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search. |

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

### import_index

```
import_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.ImportIndexRequest, dict
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


Imports an Index from an external source (e.g., BigQuery).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_import_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
config = aiplatform_v1beta1.[ConnectorConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.html)()
config.big_query_source_config.table_path = "table_path_value"
config.big_query_source_config.datapoint_field_mapping.id_column = "id_column_value"
config.big_query_source_config.datapoint_field_mapping.embedding_column = "embedding_column_value"
request = aiplatform_v1beta1.[ImportIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.html)(
name="name_value",
config=config,
)
# Make the request
operation = client.[import_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_import_index)(request=request)
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
The request object. Request message for IndexService.ImportIndex. |
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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_indexes

```
list_indexes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesPager
```


Lists Indexes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_indexes():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListIndexesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_indexes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_list_indexes)(request=request)
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
The request object. Request message for IndexService.ListIndexes. |
`parent` |
`str`
Required. The resource name of the Location from which to list the Indexes. Format: |
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
Response message for IndexService.ListIndexes. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### parse_index_path

`parse_index_path(path: str) -> typing.Dict[str, str]`


Parses a index path into its component segments.

### remove_datapoints

```
remove_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.RemoveDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.index_service.RemoveDatapointsResponse
```


Remove Datapoints from an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_remove_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RemoveDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = client.[remove_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_remove_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexService.RemoveDatapoints |
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
Response message for IndexService.RemoveDatapoints |

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

### update_index

```
update_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.UpdateIndexRequest, dict
]
] = None,
*,
index: typing.Optional[google.cloud.aiplatform_v1beta1.types.index.Index] = None,
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


Updates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
index = aiplatform_v1beta1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexRequest.html)(
index=index,
)
# Make the request
operation = client.[update_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_update_index)(request=request)
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
The request object. Request message for IndexService.UpdateIndex. |
`index` |
Required. The Index which updates the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
The update mask applies to the resource. For the |
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

### upsert_datapoints

```
upsert_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.UpsertDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.index_service.UpsertDatapointsResponse
```


Add/update Datapoints into an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_upsert_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpsertDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = client.[upsert_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_upsert_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexService.UpsertDatapoints |
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
Response message for IndexService.UpsertDatapoints |

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
