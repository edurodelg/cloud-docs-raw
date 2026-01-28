---
merged_at: 2026-01-28T15:11:44.820450
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient -->

# Class EndpointServiceAsyncClient (1.135.0)

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
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
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
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
google.cloud.aiplatform_v1.types.endpoint_service.CreateEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_create_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_create_endpoint)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.DeleteEndpointRequest,
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
from google.cloud import aiplatform_v1
async def sample_delete_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_delete_endpoint)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.DeployModelRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.DeployedModel
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
from google.cloud import aiplatform_v1
async def sample_deploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_deploy_model)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.GetEndpointRequest, dict
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
) -> google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_get_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_get_endpoint)(request=request)
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
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport
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
google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest, dict
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
google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_endpoints():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_list_endpoints)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.MutateDeployedModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.DeployedModel
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
from google.cloud import aiplatform_v1
async def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_mutate_deployed_model)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.UndeployModelRequest, dict
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
from google.cloud import aiplatform_v1
async def sample_undeploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_undeploy_model)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.UpdateEndpointRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
) -> google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_update_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = await client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.UpdateEndpointLongRunningRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint_long_running)(request=request)
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse -->

# Class ListEntityTypesResponse (1.135.0)

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`entity_types` |
`MutableSequence[`
The EntityTypes matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListEntityTypesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListEntityTypesResponse

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePersistentResourceRequest -->

# Class DeletePersistentResourceRequest (1.135.0)

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource to be deleted. Format: `projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|

## Methods

### DeletePersistentResourceRequest

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictSchemata -->

# Class PredictSchemata (1.135.0)

`PredictSchemata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.

## Attributes |
|
|---|---|
Name |
Description |
`instance_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in PredictRequest.instances, ExplainRequest.instances and BatchPredictionJob.input_config. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`parameters_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via PredictRequest.parameters, ExplainRequest.parameters and BatchPredictionJob.model_parameters. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`prediction_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via PredictResponse.predictions, ExplainResponse.explanations, and BatchPredictionJob.output_config. The schema is defined as an OpenAPI 3.0.2 `Schema Object |

## Methods

### PredictSchemata

`PredictSchemata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest -->

# Class CorroborateContentRequest (1.135.0)

`CorroborateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`content` |
Optional. Input content to corroborate, only text format is supported for now. This field is a member of `oneof` _ `_content` .
|
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. |
`parameters` |
Optional. Parameters that can be set to override default settings per request. |

## Classes

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.

## Methods

### CorroborateContentRequest

`CorroborateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionResponse -->

# Class QueryExtensionResponse (1.135.0)

`QueryExtensionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionExecutionService.QueryExtension.

## Attributes |
|
|---|---|
Name |
Description |
`steps` |
`MutableSequence[`
Steps of extension or LLM interaction, can contain function call, function response, or text response. The last step contains the final response to the query. |
`failure_message` |
`str`
Failure message if any. |

## Methods

### QueryExtensionResponse

`QueryExtensionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionExecutionService.QueryExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse -->

# Class ListPublisherModelsResponse (1.135.0)

`ListPublisherModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.ListPublisherModels.

## Attributes |
|
|---|---|
Name |
Description |
`publisher_models` |
`MutableSequence[`
List of PublisherModels in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to [ListPublisherModels.page_token][] to obtain that page. |

## Methods

### ListPublisherModelsResponse

`ListPublisherModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.ListPublisherModels.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsRequest -->

# Class ListCustomJobsRequest (1.135.0)

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the CustomJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListCustomJobsResponse.next_page_token of the previous JobService.ListCustomJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListCustomJobsRequest

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.PersistentResourceRuntimeDetail -->

# Class PersistentResourceRuntimeDetail (1.135.0)

```
PersistentResourceRuntimeDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Persistent resource based runtime detail. For more
information, refer to
[https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview)

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource_name` |
`str`
Persistent resource name. Format: `projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|
`task_resource_unavailable_wait_time_ms` |
`int`
The max time a pipeline task waits for the required CPU, memory, or accelerator resource to become available from the specified persistent resource. Default wait time is 0. |
`task_resource_unavailable_timeout_behavior` |
Specifies the behavior to take if the timeout is reached. |

## Classes

### TaskResourceUnavailableTimeoutBehavior

`TaskResourceUnavailableTimeoutBehavior(value)`


An enum that specifies the behavior to take if the timeout is reached.

## Methods

### PersistentResourceRuntimeDetail

```
PersistentResourceRuntimeDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Persistent resource based runtime detail. For more
information, refer to
[https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest -->

# Class UpdateRagEngineConfigRequest (1.135.0)

```
UpdateRagEngineConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VertexRagDataService.UpdateRagEngineConfig.

## Attribute |
|
|---|---|
Name |
Description |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. |

## Methods

### UpdateRagEngineConfigRequest

```
UpdateRagEngineConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VertexRagDataService.UpdateRagEngineConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service -->

# Package job_service (1.135.0)

API documentation for `aiplatform_v1.services.job_service`

package.

## Classes

[JobServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceAsyncClient)

A service for creating and managing Vertex AI's jobs.

[JobServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient)

A service for creating and managing Vertex AI's jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers)

API documentation for `aiplatform_v1.services.job_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeTemplateRequest -->

# Class GetNotebookRuntimeTemplateRequest (1.135.0)

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### GetNotebookRuntimeTemplateRequest

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues.Feature.FeatureValueAndTimestamp -->

# Class FeatureValueAndTimestamp (1.135.0)

`FeatureValueAndTimestamp(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature value and timestamp.

## Attributes |
|
|---|---|
Name |
Description |
`value` |
The feature value. |
`timestamp` |
`google.protobuf.timestamp_pb2.Timestamp`
The feature timestamp to store with this value. If not set, then the Feature Store server will generate a timestamp when it receives the write request. |

## Methods

### FeatureValueAndTimestamp

`FeatureValueAndTimestamp(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature value and timestamp.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Part -->

# Class Part (1.135.0)

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
`thought` |
`bool`
Indicates if the part is thought from the model. |
`thought_signature` |
`bytes`
An opaque signature for the thought so it can be reused in subsequent requests. |
`video_metadata` |
Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data. This field is a member of `oneof` _ `metadata` .
|

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsResponse -->

# Class ListOptimalTrialsResponse (1.135.0)

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

## Attribute |
|
|---|---|
Name |
Description |
`optimal_trials` |
`MutableSequence[`
The pareto-optimal Trials for multiple objective Study or the optimal trial for single objective Study. The definition of pareto-optimal can be checked in wiki page. https://en.wikipedia.org/wiki/Pareto_efficiency |

## Methods

### ListOptimalTrialsResponse

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SamplingStrategy -->

# Class SamplingStrategy (1.135.0)

`SamplingStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Sampling Strategy for logging, can be for both training and prediction dataset.

## Attribute |
|
|---|---|
Name |
Description |
`random_sample_config` |
Random sample config. Will support more sampling strategies later. |

## Classes

### RandomSampleConfig

`RandomSampleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Requests are randomly selected.

## Methods

### SamplingStrategy

`SamplingStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Sampling Strategy for logging, can be for both training and prediction dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictSchemata -->

# Class PredictSchemata (1.135.0)

`PredictSchemata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.

## Attributes |
|
|---|---|
Name |
Description |
`instance_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in PredictRequest.instances, ExplainRequest.instances and BatchPredictionJob.input_config. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`parameters_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via PredictRequest.parameters, ExplainRequest.parameters and BatchPredictionJob.model_parameters. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`prediction_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via PredictResponse.predictions, ExplainResponse.explanations, and BatchPredictionJob.output_config. The schema is defined as an OpenAPI 3.0.2 `Schema Object |

## Methods

### PredictSchemata

`PredictSchemata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers -->

# Module pagers (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest -->

# Class CorroborateContentRequest (1.135.0)

`CorroborateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`content` |
Optional. Input content to corroborate, only text format is supported for now. This field is a member of `oneof` _ `_content` .
|
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. |
`parameters` |
Optional. Parameters that can be set to override default settings per request. |

## Classes

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.

## Methods

### CorroborateContentRequest

`CorroborateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsRequest -->

# Class ListCustomJobsRequest (1.135.0)

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the CustomJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListCustomJobsResponse.next_page_token of the previous JobService.ListCustomJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListCustomJobsRequest

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDeploymentResourcePoolRequest -->

# Class DeleteDeploymentResourcePoolRequest (1.135.0)

```
DeleteDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DeleteDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DeploymentResourcePool to delete. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|

## Methods

### DeleteDeploymentResourcePoolRequest

```
DeleteDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DeleteDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse -->

# Class ListExecutionsResponse (1.135.0)

`ListExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`executions` |
`MutableSequence[`
The Executions retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListExecutionsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListExecutionsResponse

`ListExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListExecutions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitoringJobRequest -->

# Class GetModelMonitoringJobRequest (1.135.0)

```
GetModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.GetModelMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelMonitoringJob. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}/modelMonitoringJobs/{model_monitoring_job}`
|

## Methods

### GetModelMonitoringJobRequest

```
GetModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.GetModelMonitoringJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.CustomEnvironmentSpec -->

# Class CustomEnvironmentSpec (1.135.0)

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

## Attributes |
|
|---|---|
Name |
Description |
`machine_spec` |
The specification of a single machine for the execution job. |
`persistent_disk_spec` |
The specification of a persistent disk to attach for the execution job. |
`network_spec` |
The network configuration to use for the execution job. |

## Methods

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Part -->

# Class Part (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest.ModelConfig -->

# Class ModelConfig (1.135.0)

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`accept_eula` |
`bool`
Optional. Whether the user accepts the End User License Agreement (EULA) for the model. |
`hugging_face_access_token` |
`str`
Optional. The Hugging Face read access token used to access the model artifacts of gated models. |
`hugging_face_cache_enabled` |
`bool`
Optional. If true, the model will deploy with a cached version instead of directly downloading the model artifacts from Hugging Face. This is suitable for VPC-SC users with limited internet access. |
`model_display_name` |
`str`
Optional. The user-specified display name of the uploaded model. If not set, a default name will be used. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying. If not set, the default container spec will be used. |
`model_user_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. When not provided, Vertex AI will generate a value for this ID. When Model Registry model is provided, this field will be ignored. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|

## Methods

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictRequest -->

# Class DirectPredictRequest (1.135.0)

`DirectPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`inputs` |
`MutableSequence[`
The prediction input. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### DirectPredictRequest

`DirectPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardBlob -->

# Class TensorboardBlob (1.135.0)

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. A URI safe key uniquely identifying a blob. Can be used to locate the blob stored in the Cloud Storage bucket of the consumer project. |
`data` |
`bytes`
Optional. The bytes of the blob is not present unless it's returned by the ReadTensorboardBlobData endpoint. |

## Methods

### TensorboardBlob

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse -->

# Class ListEventsResponse (1.135.0)

`ListEventsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListEvents.

## Attributes |
|
|---|---|
Name |
Description |
`session_events` |
`MutableSequence[`
A list of events matching the request. Ordered by timestamp in ascending order. |
`next_page_token` |
`str`
A token, which can be sent as ListEventsRequest.page_token to retrieve the next page. Absence of this field indicates there are no subsequent pages. |

## Methods

### ListEventsResponse

`ListEventsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListEvents.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse -->

# Class ListEntityTypesResponse (1.135.0)

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`entity_types` |
`MutableSequence[`
The EntityTypes matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListEntityTypesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListEntityTypesResponse

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service -->

# Package reasoning_engine_execution_service (1.135.0)

API documentation for `aiplatform_v1.services.reasoning_engine_execution_service`

package.

## Classes

[ReasoningEngineExecutionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient)

A service for executing queries on Reasoning Engine.

[ReasoningEngineExecutionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceClient)

A service for executing queries on Reasoning Engine.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePersistentResourceRequest -->

# Class DeletePersistentResourceRequest (1.135.0)

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource to be deleted. Format: `projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|

## Methods

### DeletePersistentResourceRequest

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1beta1.services.vertex_rag_data_service.pagers`

module.

## Classes

[ListRagCorporaAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager)

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

[ListRagCorporaPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaPager)

```
ListRagCorporaPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListRagFilesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager)

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

[ListRagFilesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesPager)

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.DiscreteValueSpec -->

# Class DiscreteValueSpec (1.135.0)

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. A list of possible values. The list should be in increasing order and at least 1e-10 apart. For instance, this parameter might have possible settings of 1.5, 2.5, and 4.0. This list should not contain more than 1,000 values. |
`default_value` |
`float`
A default value for a `DISCRETE` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point. It automatically
rounds to the nearest feasible discrete point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### DiscreteValueSpec

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudyTimeConstraint -->

# Class StudyTimeConstraint (1.135.0)

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

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
`max_duration` |
`google.protobuf.duration_pb2.Duration`
Counts the wallclock time passed since the creation of this Study. This field is a member of `oneof` _ `constraint` .
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Compares the wallclock time to this time. Must use UTC timezone. This field is a member of `oneof` _ `constraint` .
|

## Methods

### StudyTimeConstraint

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs.ModelType -->

# Class ModelType (1.135.0)

A model best tailored to be used within Google Cloud, and which c annot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_CORAL_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_CORAL_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_JETSON_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

MOBILE_JETSON_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-28 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateCachedContentRequest -->

# Class UpdateCachedContentRequest (1.135.0)

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

## Attributes |
|
|---|---|
Name |
Description |
`cached_content` |
Required. The cached content to update |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. |

## Methods

### UpdateCachedContentRequest

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse.PromptFeedback -->

# Class PromptFeedback (1.135.0)

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

## Attributes |
|
|---|---|
Name |
Description |
`block_reason` |
Output only. Blocked reason. |
`safety_ratings` |
`MutableSequence[`
Output only. Safety ratings. |
`block_reason_message` |
`str`
Output only. A readable block reason message. |

## Classes

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.

## Methods

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/definition_v1 -->

# Types for Google Cloud Aiplatform V1 Schema Trainingjob Definition v1 API

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs)

#### metadata()

The metadata information.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_classification.AutoMlImageClassificationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_classification.AutoMlImageClassificationMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### base_model_id()

The ID of the `base`

model. If it is specified, the new
model will be trained based on the `base`

model.
Otherwise, the new model will be trained from scratch. The
`base`

model must be in the same Project and Location as
the new Model to train, and have the same modelType.

**Type**

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. For modelType
`cloud`

(default), the budget must be between 8,000 and
800,000 milli node hours, inclusive. The default value is
192,000 which represents one day in wall time, considering 8
nodes are used. For model types `mobile-tf-low-latency-1`

,
`mobile-tf-versatile-1`

, `mobile-tf-high-accuracy-1`

,
the training budget must be between 1,000 and 100,000 milli
node hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used.

**Type**

#### multi_label()

If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable).

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A Model best tailored to be used within
Google Cloud, and which cannot be exported.
Default.
MOBILE_TF_LOW_LATENCY_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
afterwards. Expected to have low latency, but
may have lower prediction quality than other
mobile models.
MOBILE_TF_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
with afterwards.
MOBILE_TF_HIGH_ACCURACY_1 (4):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
afterwards. Expected to have a higher latency,
but should also have a higher prediction quality
than other mobile models.
```


#### CLOUD(* = * )

#### MOBILE_TF_HIGH_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MOBILE_TF_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### base_model_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs.ModelType_ )

#### multi_label(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs)

#### metadata()

The metadata information

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_object_detection.AutoMlImageObjectDetectionInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_object_detection.AutoMlImageObjectDetectionMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. For modelType
`cloud`

(default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1`

,
`mobile-tf-versatile-1`

, `mobile-tf-high-accuracy-1`

the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used.

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD_HIGH_ACCURACY_1 (1):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Expected to have a higher latency, but should
also have a higher prediction quality than other
cloud models.
CLOUD_LOW_LATENCY_1 (2):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Expected to have a low latency, but may have
lower prediction quality than other cloud
models.
MOBILE_TF_LOW_LATENCY_1 (3):
A model that, in addition to being available
within Google Cloud can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
Expected to have low latency, but may have lower
prediction quality than other mobile models.
MOBILE_TF_VERSATILE_1 (4):
A model that, in addition to being available
within Google Cloud can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
MOBILE_TF_HIGH_ACCURACY_1 (5):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
Expected to have a higher latency, but should
also have a higher prediction quality than other
mobile models.
```


#### CLOUD_HIGH_ACCURACY_1(* = * )

#### CLOUD_LOW_LATENCY_1(* = * )

#### MOBILE_TF_HIGH_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MOBILE_TF_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs)

#### metadata()

The metadata information.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_segmentation.AutoMlImageSegmentationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_segmentation.AutoMlImageSegmentationMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. Or actaul_wall_clock_hours =
train_budget_milli_node_hours / (number_of_nodes_involved *
1000) For modelType `cloud-high-accuracy-1`

(default),
the budget must be between 20,000 and 2,000,000 milli node
hours, inclusive. The default value is 192,000 which
represents one day in wall time (1000 milli * 24 hours * 8
nodes).

**Type**

#### base_model_id()

The ID of the `base`

model. If it is specified, the new
model will be trained based on the `base`

model.
Otherwise, the new model will be trained from scratch. The
`base`

model must be in the same Project and Location as
the new Model to train, and have the same modelType.

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD_HIGH_ACCURACY_1 (1):
A model to be used via prediction calls to
uCAIP API. Expected to have a higher latency,
but should also have a higher prediction quality
than other models.
CLOUD_LOW_ACCURACY_1 (2):
A model to be used via prediction calls to
uCAIP API. Expected to have a lower latency but
relatively lower prediction quality.
MOBILE_TF_LOW_LATENCY_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow model
and used on a mobile or edge device afterwards.
Expected to have low latency, but may have lower
prediction quality than other mobile models.
```


#### CLOUD_HIGH_ACCURACY_1(* = * )

#### CLOUD_LOW_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### base_model_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Tables Model.

#### inputs()

The input parameters of this TrainingJob.

#### metadata()

The metadata information.

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### optimization_objective_recall_value()

Required when optimization_objective is “maximize-precision-at-recall”. Must be between 0 and 1, inclusive.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `additional_optimization_objective_config`

.

**Type**

#### optimization_objective_precision_value()

Required when optimization_objective is “maximize-recall-at-precision”. Must be between 0 and 1, inclusive.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `additional_optimization_objective_config`

.

**Type**

#### prediction_type()

The type of prediction the Model is to produce. “classification” - Predict one out of multiple target values is picked for each row.

“regression” - Predict a value based on its


relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings.

**Type**

#### target_column()

The column name of the target column that the model is to predict.

**Type**

#### transformations()

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using “.” as the delimiter.

**Type**MutableSequence[

[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation)]

#### optimization_objective()

Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set.

The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used.

classification (binary):

“maximize-au-roc” (default) - Maximize the


area under the receiver operating characteristic (ROC) curve. “minimize-log-loss” - Minimize log loss.

“maximize-au-prc” - Maximize the area under


the precision-recall curve. “maximize-precision-at-recall” - Maximize precision for a specified recall value. “maximize-recall-at-precision” - Maximize recall for a specified precision value.

classification (multi-class):

“minimize-log-loss” (default) - Minimize log


loss.

regression:

“minimize-rmse” (default) - Minimize


root-mean-squared error (RMSE). “minimize-mae”

Minimize mean-absolute error (MAE). “minimize-rmsle” - Minimize root-mean-squared log error (RMSLE).

**Type**

#### train_budget_milli_node_hours()

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend’s discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won’t be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used.

**Type**

#### weight_column_name()

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

**Type**

#### export_evaluated_data_items_config()

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig)

#### additional_experiments()

Additional experiment flags for the Tables training pipeline.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*class* Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### auto()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### timestamp()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

*class* AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will infer the proper transformation based on the statistic of dataset.

#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as categorical array and performs following transformation functions.

For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.

Empty arrays treated as an embedding of zeroes.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The categorical string as is–no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the “unknown” category. The “unknown” category gets its own special lookup index and resulting embedding.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as numerical array and performs following transformation functions.

All transformations for Numerical types applied to the average of the all elements.

The average of empty arrays is treated as zero.


#### column_name()

**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


#### column_name()

**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as text array and performs following transformation functions.

Concatenate all text values in the array into a single text value using a space (” “) as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.

Empty arrays treated as an empty text.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The text as is–no change to case, punctuation, spelling, tense, and so on.

Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.

Tokenization is based on unicode script boundaries.

Missing values get their own lookup index and resulting embedding.

Stop-words receive no special treatment and are not removed.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the

timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


#### column_name()

**Type**

#### time_format()

The format in which that time field is expressed. The time_format must either be one of:

`unix-seconds`

`unix-milliseconds`

`unix-microseconds`

`unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch); or be written in`strftime`

syntax. If time_format is not set, then the default format is RFC 3339`date-time`

format, where`time-offset`

=`"Z"`

(e.g. 1985-04-12T23:20:50.52Z)**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### time_format(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### auto(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.AutoTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.AutoTransformation_ )

#### categorical(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.CategoricalTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation_ )

#### numeric(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.NumericTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericTransformation_ )

#### repeated_categorical(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation_ )

#### repeated_numeric(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.NumericArrayTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation_ )

#### repeated_text(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.TextArrayTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TextArrayTransformation_ )

#### text(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.TextTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TextTransformation_ )

#### timestamp(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.TimestampTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TimestampTransformation_ )

#### additional_experiments(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### export_evaluated_data_items_config(*: gcastd_export_evaluated_data_items_config.ExportEvaluatedDataItemsConfi* )

#### optimization_objective(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### optimization_objective_precision_value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### optimization_objective_recall_value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### prediction_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### target_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### train_budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### transformations(*: MutableSequence[[Transformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation)_ )

#### weight_column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Model metadata specific to AutoML Tables.

#### train_cost_milli_node_hours()

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

**Type**

#### train_cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Classification Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_text_classification.AutoMlTextClassificationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### multi_label()

**Type**

#### multi_label(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs


#### inputs(*: google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_text_extraction.AutoMlTextExtractionInput* )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_text_sentiment.AutoMlTextSentimentInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentimentInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### sentiment_max()

A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive).

**Type**

#### sentiment_max(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognition(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_video_action_recognition.AutoMlVideoActionRecognitionInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which c annot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_JETSON_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) to a Jetson device
afterwards.
MOBILE_CORAL_VERSATILE_1 (4):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a Coral device
afterwards.
```


#### CLOUD(* = * )

#### MOBILE_CORAL_VERSATILE_1(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video Classification Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_video_classification.AutoMlVideoClassificationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_JETSON_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) to a Jetson device
afterwards.
```


#### CLOUD(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_video_object_tracking.AutoMlVideoObjectTrackingInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which c annot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_CORAL_VERSATILE_1 (3):
A versatile model that is meant to be
exported (see ModelService.ExportModel) and used
on a Google Coral device.
MOBILE_CORAL_LOW_LATENCY_1 (4):
A model that trades off quality for low
latency, to be exported (see
ModelService.ExportModel) and used on a Google
Coral device.
MOBILE_JETSON_VERSATILE_1 (5):
A versatile model that is meant to be
exported (see ModelService.ExportModel) and used
on an NVIDIA Jetson device.
MOBILE_JETSON_LOW_LATENCY_1 (6):
A model that trades off quality for low
latency, to be exported (see
ModelService.ExportModel) and used on an NVIDIA
Jetson device.
```


#### CLOUD(* = * )

#### MOBILE_CORAL_LOW_LATENCY_1(* = * )

#### MOBILE_CORAL_VERSATILE_1(* = * )

#### MOBILE_JETSON_LOW_LATENCY_1(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Configuration for exporting test set predictions to a BigQuery table.

#### destination_bigquery_uri()

URI of desired destination BigQuery table. Expected format: bq://<project_id>:<dataset_id>:

If not specified, then results are exported to the following auto-created BigQuery table: <project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd’T’HH_mm_ss_SSS’Z’>.evaluated_examples

**Type**

#### override_existing_table()

If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails.

**Type**

#### destination_bigquery_uri(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### override_existing_table(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView -->

# Class FeatureView (1.135.0)

`FeatureView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig.

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
`big_query_source` |
Optional. Configures how data is supposed to be extracted from a BigQuery source to be loaded onto the FeatureOnlineStore. This field is a member of `oneof` _ `source` .
|
`feature_registry_source` |
Optional. Configures the features from a Feature Registry source that need to be loaded onto the FeatureOnlineStore. This field is a member of `oneof` _ `source` .
|
`vertex_rag_source` |
Optional. The Vertex RAG Source that the FeatureView is linked to. This field is a member of `oneof` _ `source` .
|
`name` |
`str`
Identifier. Name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureView was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureView was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureViews. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`sync_config` |
Configures when data is to be synced/updated for this FeatureView. At the end of the sync the latest featureValues for each entityId of this FeatureView are made ready for online serving. |
`index_config` |
Optional. Configuration for index preparation for vector search. It contains the required configurations to create an index from source data, so that approximate nearest neighbor (a.k.a ANN) algorithms search can be performed during online serving. |
`optimized_config` |
Optional. Configuration for FeatureView created under Optimized FeatureOnlineStore. |
`service_agent_type` |
Optional. Service agent type used during data sync. By default, the Vertex AI Service Agent is used. When using an IAM Policy to isolate this FeatureView within a project, a separate service account should be provisioned by setting this field to `SERVICE_AGENT_TYPE_FEATURE_VIEW` . This will
generate a separate service account to access the BigQuery
source table.
|
`service_account_email` |
`str`
Output only. A Service Account unique to this FeatureView. The role bigquery.dataViewer should be granted to this service account to allow Vertex AI Feature Store to sync data to the online store. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`bigtable_metadata` |
Metadata containing information about the Cloud Bigtable. |

## Classes

### BigQuerySource

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.

### FeatureRegistrySource

`FeatureRegistrySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Feature Registry source for features that need to be synced to Online Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### IndexConfig

`IndexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for vector indexing.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

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

### OptimizedConfig

`OptimizedConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for FeatureViews created in Optimized FeatureOnlineStore.

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during data sync.

### SyncConfig

`SyncConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Sync. Only one option is set.

### VertexRagSource

`VertexRagSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Vertex Rag source for features that need to be synced to Online Store.

## Methods

### FeatureView

`FeatureView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.ModelConfig -->

# Class ModelConfig (1.135.0)

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`accept_eula` |
`bool`
Optional. Whether the user accepts the End User License Agreement (EULA) for the model. |
`hugging_face_access_token` |
`str`
Optional. The Hugging Face read access token used to access the model artifacts of gated models. |
`hugging_face_cache_enabled` |
`bool`
Optional. If true, the model will deploy with a cached version instead of directly downloading the model artifacts from Hugging Face. This is suitable for VPC-SC users with limited internet access. |
`model_display_name` |
`str`
Optional. The user-specified display name of the uploaded model. If not set, a default name will be used. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying. If not set, the default container spec will be used. |
`model_user_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. When not provided, Vertex AI will generate a value for this ID. When Model Registry model is provided, this field will be ignored. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|

## Methods

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest -->

# Class GenerateFetchAccessTokenRequest (1.135.0)

```
GenerateFetchAccessTokenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

## Attribute |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|

## Methods

### GenerateFetchAccessTokenRequest

```
GenerateFetchAccessTokenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenResponse -->

# Class GenerateFetchAccessTokenResponse (1.135.0)

```
GenerateFetchAccessTokenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

## Attributes |
|
|---|---|
Name |
Description |
`access_token` |
`str`
The OAuth 2.0 access token. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Token expiration time. This is always set |

## Methods

### GenerateFetchAccessTokenResponse

```
GenerateFetchAccessTokenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers -->

# Module pagers (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata -->

# Class InputMetadata (1.135.0)

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

## Attributes |
|
|---|---|
Name |
Description |
`input_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Baseline inputs for this feature. If no baseline is specified, Vertex AI chooses the baseline for this feature. If multiple baselines are specified, Vertex AI returns the average attributions across them in Attribution.feature_attributions. For Vertex AI-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor. For custom images, the element of the baselines must be in the same format as the feature's input in the instance[]. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. |
`input_tensor_name` |
`str`
Name of the input tensor for this feature. Required and is only applicable to Vertex AI-provided images for Tensorflow. |
`encoding` |
Defines how the feature is encoded into the input tensor. Defaults to IDENTITY. |
`modality` |
`str`
Modality of the feature. Valid values are: numeric, image. Defaults to numeric. |
`feature_value_domain` |
The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized. |
`indices_tensor_name` |
`str`
Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`dense_shape_tensor_name` |
`str`
Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`index_feature_mapping` |
`MutableSequence[str]`
A list of feature names for each index in the input tensor. Required when the input InputMetadata.encoding is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR. |
`encoded_tensor_name` |
`str`
Encoded tensor is a transformation of the input tensor. Must be provided if choosing [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution] or [XRAI attribution][google.cloud.aiplatform.v1.ExplanationParameters.xrai_attribution] and the input tensor is not differentiable. An encoded tensor is generated if the input tensor is encoded by a lookup table. |
`encoded_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
A list of baselines for the encoded tensor. The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Vertex AI broadcasts to the same shape as the encoded tensor. |
`visualization` |
Visualization configurations for image explanation. |
`group_name` |
`str`
Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in Attribution.feature_attributions, keyed by the group name. |

## Classes

### Encoding

`Encoding(value)`


Defines how a feature is encoded. Defaults to IDENTITY.

```
::
input = [27, 6.0, 150]
index_feature_mapping = ["age", "height", "weight"]
BAG_OF_FEATURES_SPARSE (3):
The tensor represents a bag of features where each index
maps to a feature. Zero values in the tensor indicates
feature being non-existent.
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [2, 0, 5, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
INDICATOR (4):
The tensor is a list of binaries representing whether a
feature exists or not (1 indicates existence).
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [1, 0, 1, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
COMBINED_EMBEDDING (5):
The tensor is encoded into a 1-dimensional array represented
by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]
CONCAT_EMBEDDING (6):
Select this encoding when the input tensor is encoded into a
2-dimensional array represented by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. The first dimension of
the encoded tensor's shape is the same as the input tensor's
shape. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
[0.2, 0.1, 0.4, 0.3, 0.5],
[0.5, 0.1, 0.3, 0.5, 0.4],
[0.5, 0.3, 0.1, 0.2, 0.4],
[0.4, 0.3, 0.2, 0.5, 0.1]]
```


### FeatureValueDomain

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

### Visualization

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

## Methods

### InputMetadata

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelDeploymentMonitoringJobOperationMetadata -->

# Class UpdateModelDeploymentMonitoringJobOperationMetadata (1.135.0)

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateModelDeploymentMonitoringJobOperationMetadata

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualitySpec -->

# Class PairwiseQuestionAnsweringQualitySpec (1.135.0)

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

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

### PairwiseQuestionAnsweringQualitySpec

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest -->

# Class GetNotebookRuntimeTemplateRequest (1.135.0)

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### GetNotebookRuntimeTemplateRequest

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsResponse -->

# Class ListOptimalTrialsResponse (1.135.0)

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

## Attribute |
|
|---|---|
Name |
Description |
`optimal_trials` |
`MutableSequence[`
The pareto-optimal Trials for multiple objective Study or the optimal trial for single objective Study. The definition of pareto-optimal can be checked in wiki page. https://en.wikipedia.org/wiki/Pareto_efficiency |

## Methods

### ListOptimalTrialsResponse

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers -->

# Module pagers (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig -->

# Class AuthConfig (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudyTimeConstraint -->

# Class StudyTimeConstraint (1.135.0)

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

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
`max_duration` |
`google.protobuf.duration_pb2.Duration`
Counts the wallclock time passed since the creation of this Study. This field is a member of `oneof` _ `constraint` .
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Compares the wallclock time to this time. Must use UTC timezone. This field is a member of `oneof` _ `constraint` .
|

## Methods

### StudyTimeConstraint

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.DiscreteValueSpec -->

# Class DiscreteValueSpec (1.135.0)

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. A list of possible values. The list should be in increasing order and at least 1e-10 apart. For instance, this parameter might have possible settings of 1.5, 2.5, and 4.0. This list should not contain more than 1,000 values. |
`default_value` |
`float`
A default value for a `DISCRETE` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point. It automatically
rounds to the nearest feasible discrete point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### DiscreteValueSpec

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.135.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse -->

# Class ListTensorboardsResponse (1.135.0)

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboards` |
`MutableSequence[`
The Tensorboards mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardsResponse

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig.TreeAHConfig -->

# Class TreeAHConfig (1.135.0)

`TreeAHConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`leaf_node_embedding_count` |
`int`
Optional. Number of embeddings on each leaf node. The default value is 1000 if not set. This field is a member of `oneof` _ `_leaf_node_embedding_count` .
|

## Methods

### TreeAHConfig

`TreeAHConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitorRequest -->

# Class DeleteModelMonitorRequest (1.135.0)

`DeleteModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.DeleteModelMonitor.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelMonitor resource to be deleted. Format: `projects/{project}/locations/{location}/modelMonitords/{model_monitor}`
|
`force` |
`bool`
Optional. Force delete the model monitor with schedules. |

## Methods

### DeleteModelMonitorRequest

`DeleteModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.DeleteModelMonitor.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardBlob -->

# Class TensorboardBlob (1.135.0)

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. A URI safe key uniquely identifying a blob. Can be used to locate the blob stored in the Cloud Storage bucket of the consumer project. |
`data` |
`bytes`
Optional. The bytes of the blob is not present unless it's returned by the ReadTensorboardBlobData endpoint. |

## Methods

### TensorboardBlob

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureViewSyncRequest -->

# Class GetFeatureViewSyncRequest (1.135.0)

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureViewSync resource. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### GetFeatureViewSyncRequest

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample -->

# Class StoredContentsExample (1.135.0)

`StoredContentsExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ContentsExample to be used with GenerateContent alongside information required for storage and retrieval with Example Store.

## Attributes |
|
|---|---|
Name |
Description |
`search_key` |
`str`
Optional. (Optional) the search key used for retrieval. If not provided at upload-time, the search key will be generated from `contents_example.contents` using the
method provided by `search_key_generation_method` . The
generated search key will be included in retrieved examples.
|
`contents_example` |
Required. The example to be used with GenerateContent. |
`search_key_generation_method` |
Optional. The method used to generate the search key from `contents_example.contents` . This is ignored when
uploading an example if `search_key` is provided.
|

## Classes

### SearchKeyGenerationMethod

`SearchKeyGenerationMethod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options for generating the search key from the conversation history.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### StoredContentsExample

`StoredContentsExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ContentsExample to be used with GenerateContent alongside information required for storage and retrieval with Example Store.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesPager (1.135.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
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

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesPager

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTrackingInputs.ModelType -->

# Class ModelType (1.135.0)

A model best tailored to be used within Google Cloud, and which c annot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_CORAL_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_CORAL_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_JETSON_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

MOBILE_JETSON_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-28 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextChildrenRequest -->

# Class AddContextChildrenRequest (1.135.0)

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### AddContextChildrenRequest

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.CategoricalValueCondition -->

# Class CategoricalValueCondition (1.135.0)

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categorical_value_spec` of parent parameter.
|

## Methods

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1.services.pipeline_service.pagers`

module.

## Classes

[ListPipelineJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager)

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

[ListPipelineJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsPager)

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager)

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
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


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse) object, and
provides an `__aiter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1.services.job_service.pagers`

module.

## Classes

[ListBatchPredictionJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager)

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
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


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListBatchPredictionJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsPager)

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

[ListCustomJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsAsyncPager)

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse) object, and
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

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListCustomJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsPager)

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsAsyncPager)

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

[ListDataLabelingJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsPager)

```
ListDataLabelingJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse,
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
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse) object, and
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

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListHyperparameterTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager)

```
ListHyperparameterTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListHyperparameterTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsPager)

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsAsyncPager)

```
ListModelDeploymentMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager)

```
ListModelDeploymentMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsAsyncPager)

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsPager)

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

[ListNasTrialDetailsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsAsyncPager)

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

[ListNasTrialDetailsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsPager)

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse) object, and
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

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchModelDeploymentMonitoringStatsAnomaliesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingInput -->

# Class RubricBasedInstructionFollowingInput (1.135.0)

```
RubricBasedInstructionFollowingInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instance and metric spec for RubricBasedInstructionFollowing metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for RubricBasedInstructionFollowing metric. |
`instance` |
Required. Instance for RubricBasedInstructionFollowing metric. |

## Methods

### RubricBasedInstructionFollowingInput

```
RubricBasedInstructionFollowingInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instance and metric spec for RubricBasedInstructionFollowing metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentResponse.PromptFeedback -->

# Class PromptFeedback (1.135.0)

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

## Attributes |
|
|---|---|
Name |
Description |
`block_reason` |
Output only. Blocked reason. |
`safety_ratings` |
`MutableSequence[`
Output only. Safety ratings. |
`block_reason_message` |
`str`
Output only. A readable block reason message. |

## Classes

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.

## Methods

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateCachedContentRequest -->

# Class UpdateCachedContentRequest (1.135.0)

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

## Attributes |
|
|---|---|
Name |
Description |
`cached_content` |
Required. The cached content to update |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. |

## Methods

### UpdateCachedContentRequest

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DiskSpec -->

# Class DiskSpec (1.135.0)

`DiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of disk options.

## Attributes |
|
|---|---|
Name |
Description |
`boot_disk_type` |
`str`
Type of the boot disk. For non-A3U machines, the default value is "pd-ssd", for A3U machines, the default value is "hyperdisk-balanced". Valid values: "pd-ssd" (Persistent Disk Solid State Drive), "pd-standard" (Persistent Disk Hard Disk Drive) or "hyperdisk-balanced". |
`boot_disk_size_gb` |
`int`
Size in GB of the boot disk (default is 100GB). |

## Methods

### DiskSpec

`DiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of disk options.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest -->

# Class GetFeatureMonitorJobRequest (1.135.0)

`GetFeatureMonitorJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.GetFeatureMonitorJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureMonitorJob resource. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}/featureMonitorJobs/{feature_monitor_job}`
|

## Methods

### GetFeatureMonitorJobRequest

`GetFeatureMonitorJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.GetFeatureMonitorJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobOperationMetadata -->

# Class UpdateModelDeploymentMonitoringJobOperationMetadata (1.135.0)

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateModelDeploymentMonitoringJobOperationMetadata

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ShieldedVmConfig -->

# Class ShieldedVmConfig (1.135.0)

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

## Attribute |
|
|---|---|
Name |
Description |
`enable_secure_boot` |
`bool`
Defines whether the instance has `Secure Boot |

## Methods

### ShieldedVmConfig

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopNotebookRuntimeRequest -->

# Class StopNotebookRuntimeRequest (1.135.0)

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StopNotebookRuntimeRequest

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.ExplanationConfig -->

# Class ExplanationConfig (1.135.0)

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

## Attributes |
|
|---|---|
Name |
Description |
`enable_feature_attributes` |
`bool`
If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Vertex AI will log the feature attributions from explain response and do the skew/drift detection for them. |
`explanation_baseline` |
Predictions generated by the BatchPredictionJob using baseline dataset. |

## Classes

### ExplanationBaseline

`ExplanationBaseline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output from BatchPredictionJob for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrainingPipelineRequest -->

# Class CreateTrainingPipelineRequest (1.135.0)

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: `projects/{project}/locations/{location}`
|
`training_pipeline` |
Required. The TrainingPipeline to create. |

## Methods

### CreateTrainingPipelineRequest

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PostStartupScriptConfig.PostStartupScriptBehavior -->

# Class PostStartupScriptBehavior (1.135.0)

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

## Enums |
|
|---|---|
Name |
Description |
`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` |
Unspecified post startup script behavior. |
`RUN_ONCE` |
Run post startup script after runtime is started. |
`RUN_EVERY_START` |
Run post startup script after runtime is stopped. |
`DOWNLOAD_AND_RUN_EVERY_START` |
Download and run post startup script every time runtime is started. |

## Methods

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelResponse -->

# Class ExportPublisherModelResponse (1.135.0)

```
ExportPublisherModelResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelGardenService.ExportPublisherModel.

## Attributes |
|
|---|---|
Name |
Description |
`publisher_model` |
`str`
The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}`
|
`destination_uri` |
`str`
The destination uri of the model weights. |

## Methods

### ExportPublisherModelResponse

```
ExportPublisherModelResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelGardenService.ExportPublisherModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateReasoningEngineRequest -->

# Class UpdateReasoningEngineRequest (1.135.0)

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. |

## Methods

### UpdateReasoningEngineRequest

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagRetrievalConfig.Filter -->

# Class Filter (1.135.0)

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

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
`vector_distance_threshold` |
`float`
Optional. Only returns contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`vector_similarity_threshold` |
`float`
Optional. Only returns contexts with vector similarity larger than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`metadata_filter` |
`str`
Optional. String for metadata filtering. |

## Methods

### Filter

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsRequest -->

# Class ListModelDeploymentMonitoringJobsRequest (1.135.0)

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read |

## Methods

### ListModelDeploymentMonitoringJobsRequest

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualitySpec -->

# Class PairwiseQuestionAnsweringQualitySpec (1.135.0)

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

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

### PairwiseQuestionAnsweringQualitySpec

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse -->

# Class ListTensorboardsResponse (1.135.0)

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboards` |
`MutableSequence[`
The Tensorboards mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardsResponse

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.135.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetAnnotationSpecRequest -->

# Class GetAnnotationSpecRequest (1.135.0)

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the AnnotationSpec resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/annotationSpecs/{annotation_spec}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetAnnotationSpecRequest

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.MetricSpec.SafetyMetricConfig -->

# Class SafetyMetricConfig (1.135.0)

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`safety_threshold` |
`float`
Safety threshold (boundary value between safe and unsafe). NOTE that if you leave SafetyMetricConfig unset, a default value of 0 will be used. |
`desired_min_safe_trials_fraction` |
`float`
Desired minimum fraction of safe trials (over total number of trials) that should be targeted by the algorithm at any time during the study (best effort). This should be between 0.0 and 1.0 and a value of 0.0 means that there is no minimum and an algorithm proceeds without targeting any specific fraction. A value of 1.0 means that the algorithm attempts to only Suggest safe Trials. This field is a member of `oneof` _ `_desired_min_safe_trials_fraction` .
|

## Methods

### SafetyMetricConfig

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1beta1.services.example_store_service.pagers`

module.

## Classes

[FetchExamplesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesAsyncPager)

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

[FetchExamplesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesPager)

```
FetchExamplesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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


A pager for iterating through `fetch_examples`

requests.

This class thinly wraps an initial
[FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse) object, and
provides an `__iter__`

method to iterate through its
`examples`

field.

If there are more pages, the `__iter__`

method will make additional
`FetchExamples`

requests and continue to iterate
through the `examples`

field on the
corresponding responses.

All the usual [FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExampleStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresAsyncPager)

```
ListExampleStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
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


A pager for iterating through `list_example_stores`

requests.

This class thinly wraps an initial
[ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`example_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExampleStores`

requests and continue to iterate
through the `example_stores`

field on the
corresponding responses.

All the usual [ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExampleStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata -->

# Class InputMetadata (1.135.0)

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

## Attributes |
|
|---|---|
Name |
Description |
`input_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Baseline inputs for this feature. If no baseline is specified, Vertex AI chooses the baseline for this feature. If multiple baselines are specified, Vertex AI returns the average attributions across them in Attribution.feature_attributions. For Vertex AI-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor. For custom images, the element of the baselines must be in the same format as the feature's input in the instance[]. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`input_tensor_name` |
`str`
Name of the input tensor for this feature. Required and is only applicable to Vertex AI-provided images for Tensorflow. |
`encoding` |
Defines how the feature is encoded into the input tensor. Defaults to IDENTITY. |
`modality` |
`str`
Modality of the feature. Valid values are: numeric, image. Defaults to numeric. |
`feature_value_domain` |
The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized. |
`indices_tensor_name` |
`str`
Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`dense_shape_tensor_name` |
`str`
Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`index_feature_mapping` |
`MutableSequence[str]`
A list of feature names for each index in the input tensor. Required when the input InputMetadata.encoding is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR. |
`encoded_tensor_name` |
`str`
Encoded tensor is a transformation of the input tensor. Must be provided if choosing [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution] or [XRAI attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.xrai_attribution] and the input tensor is not differentiable. An encoded tensor is generated if the input tensor is encoded by a lookup table. |
`encoded_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
A list of baselines for the encoded tensor. The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Vertex AI broadcasts to the same shape as the encoded tensor. |
`visualization` |
Visualization configurations for image explanation. |
`group_name` |
`str`
Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in Attribution.feature_attributions, keyed by the group name. |

## Classes

### Encoding

`Encoding(value)`


Defines how a feature is encoded. Defaults to IDENTITY.

```
::
input = [27, 6.0, 150]
index_feature_mapping = ["age", "height", "weight"]
BAG_OF_FEATURES_SPARSE (3):
The tensor represents a bag of features where each index
maps to a feature. Zero values in the tensor indicates
feature being non-existent.
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [2, 0, 5, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
INDICATOR (4):
The tensor is a list of binaries representing whether a
feature exists or not (1 indicates existence).
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [1, 0, 1, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
COMBINED_EMBEDDING (5):
The tensor is encoded into a 1-dimensional array represented
by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]
CONCAT_EMBEDDING (6):
Select this encoding when the input tensor is encoded into a
2-dimensional array represented by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. The first dimension of
the encoded tensor's shape is the same as the input tensor's
shape. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
[0.2, 0.1, 0.4, 0.3, 0.5],
[0.5, 0.1, 0.3, 0.5, 0.4],
[0.5, 0.3, 0.1, 0.2, 0.4],
[0.4, 0.3, 0.2, 0.5, 0.1]]
```


### FeatureValueDomain

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

### Visualization

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

## Methods

### InputMetadata

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighbors.Neighbor -->

# Class Neighbor (1.135.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
The id of the similar entity. |
`distance` |
`float`
The distance between the neighbor and the query vector. |
`entity_key_values` |
The attributes of the neighbor, e.g. filters, crowding and metadata Note that full entities are returned only when "return_full_entity" is set to true. Otherwise, only the "entity_id" and "distance" fields are populated. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest -->

# Class RebootPersistentResourceRequest (1.135.0)

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: `projects/{project_id_or_number}/locations/{location_id}/persistentResources/{persistent_resource_id}`
|

## Methods

### RebootPersistentResourceRequest

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse -->

# Class ListModelEvaluationsResponse (1.135.0)

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

## Attributes |
|
|---|---|
Name |
Description |
`model_evaluations` |
`MutableSequence[`
List of ModelEvaluations in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelEvaluationsRequest.page_token to obtain that page. |

## Methods

### ListModelEvaluationsResponse

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagContexts -->

# Class RagContexts (1.135.0)

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

## Attribute |
|
|---|---|
Name |
Description |
`contexts` |
`MutableSequence[`
All its contexts. |

## Classes

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagContexts

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.ExplanationConfig -->

# Class ExplanationConfig (1.135.0)

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

## Attributes |
|
|---|---|
Name |
Description |
`enable_feature_attributes` |
`bool`
If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Vertex AI will log the feature attributions from explain response and do the skew/drift detection for them. |
`explanation_baseline` |
Predictions generated by the BatchPredictionJob using baseline dataset. |

## Classes

### ExplanationBaseline

`ExplanationBaseline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output from BatchPredictionJob for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualityInstance -->

# Class PairwiseQuestionAnsweringQualityInstance (1.135.0)

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the candidate model. This field is a member of `oneof` _ `_prediction` .
|
`baseline_prediction` |
`str`
Required. Output of the baseline model. This field is a member of `oneof` _ `_baseline_prediction` .
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

### PairwiseQuestionAnsweringQualityInstance

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewSyncRequest -->

# Class GetFeatureViewSyncRequest (1.135.0)

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureViewSync resource. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### GetFeatureViewSyncRequest

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentiment -->

# Class AutoMlTextSentiment (1.135.0)

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig.Filter -->

# Class Filter (1.135.0)

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

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
`vector_distance_threshold` |
`float`
Optional. Only returns contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`vector_similarity_threshold` |
`float`
Optional. Only returns contexts with vector similarity larger than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`metadata_filter` |
`str`
Optional. String for metadata filtering. |

## Methods

### Filter

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsRequest -->

# Class ListModelDeploymentMonitoringJobsRequest (1.135.0)

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read |

## Methods

### ListModelDeploymentMonitoringJobsRequest

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetRequest -->

# Class UpdateExplanationDatasetRequest (1.135.0)

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The resource name of the Model to update. Format: `projects/{project}/locations/{location}/models/{model}`
|
`examples` |
The example config containing the location of the dataset. |

## Methods

### UpdateExplanationDatasetRequest

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextChildrenRequest -->

# Class AddContextChildrenRequest (1.135.0)

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### AddContextChildrenRequest

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensorboard -->

# Class Tensorboard (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.MetricSpec.SafetyMetricConfig -->

# Class SafetyMetricConfig (1.135.0)

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`safety_threshold` |
`float`
Safety threshold (boundary value between safe and unsafe). NOTE that if you leave SafetyMetricConfig unset, a default value of 0 will be used. |
`desired_min_safe_trials_fraction` |
`float`
Desired minimum fraction of safe trials (over total number of trials) that should be targeted by the algorithm at any time during the study (best effort). This should be between 0.0 and 1.0 and a value of 0.0 means that there is no minimum and an algorithm proceeds without targeting any specific fraction. A value of 1.0 means that the algorithm attempts to only Suggest safe Trials. This field is a member of `oneof` _ `_desired_min_safe_trials_fraction` .
|

## Methods

### SafetyMetricConfig

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.CategoricalValueCondition -->

# Class CategoricalValueCondition (1.135.0)

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categorical_value_spec` of parent parameter.
|

## Methods

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateReasoningEngineRequest -->

# Class CreateReasoningEngineRequest (1.135.0)

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the ReasoningEngine in. Format: `projects/{project}/locations/{location}`
|
`reasoning_engine` |
Required. The ReasoningEngine to create. |

## Methods

### CreateReasoningEngineRequest

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LineageSubgraph -->

# Class LineageSubgraph (1.135.0)

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
The Artifact nodes in the subgraph. |
`executions` |
`MutableSequence[`
The Execution nodes in the subgraph. |
`events` |
`MutableSequence[`
The Event edges between Artifacts and Executions in the subgraph. |

## Methods

### LineageSubgraph

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateReasoningEngineRequest -->

# Class UpdateReasoningEngineRequest (1.135.0)

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. |

## Methods

### UpdateReasoningEngineRequest

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluatedAnnotationExplanation -->

# Class EvaluatedAnnotationExplanation (1.135.0)

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

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
`explanation` |
Explanation attribution response details. |

## Methods

### EvaluatedAnnotationExplanation

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest -->

# Class CreateTrainingPipelineRequest (1.135.0)

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: `projects/{project}/locations/{location}`
|
`training_pipeline` |
Required. The TrainingPipeline to create. |

## Methods

### CreateTrainingPipelineRequest

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensorboard -->

# Class Tensorboard (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelHyperparameterTuningJobRequest -->

# Class CancelHyperparameterTuningJobRequest (1.135.0)

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### CancelHyperparameterTuningJobRequest

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ShieldedVmConfig -->

# Class ShieldedVmConfig (1.135.0)

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

## Attribute |
|
|---|---|
Name |
Description |
`enable_secure_boot` |
`bool`
Defines whether the instance has `Secure Boot |

## Methods

### ShieldedVmConfig

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation -->

# Class CategoricalArrayTransformation (1.135.0)

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

## Methods

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityInstance -->

# Class PairwiseQuestionAnsweringQualityInstance (1.135.0)

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the candidate model. This field is a member of `oneof` _ `_prediction` .
|
`baseline_prediction` |
`str`
Required. Output of the baseline model. This field is a member of `oneof` _ `_baseline_prediction` .
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

### PairwiseQuestionAnsweringQualityInstance

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest -->

# Class StopNotebookRuntimeRequest (1.135.0)

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StopNotebookRuntimeRequest

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.GcsNotebookSource -->

# Class GcsNotebookSource (1.135.0)

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
|
`generation` |
`str`
The version of the Cloud Storage object to read. If unset, the current version of the object is read. See https://cloud.google.com/storage/docs/metadata#generation-number. |

## Methods

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1beta1.services.feature_registry_service.pagers`

module.

## Classes

[ListFeatureGroupsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager)

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureGroupsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsPager)

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

[ListFeatureMonitorJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsAsyncPager)

```
ListFeatureMonitorJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
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


A pager for iterating through `list_feature_monitor_jobs`

requests.

This class thinly wraps an initial
[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_monitor_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureMonitorJobs`

requests and continue to iterate
through the `feature_monitor_jobs`

field on the
corresponding responses.

All the usual [ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsPager)

```
ListFeatureMonitorJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
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


A pager for iterating through `list_feature_monitor_jobs`

requests.

This class thinly wraps an initial
[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_monitor_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureMonitorJobs`

requests and continue to iterate
through the `feature_monitor_jobs`

field on the
corresponding responses.

All the usual [ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsAsyncPager)

```
ListFeatureMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
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


A pager for iterating through `list_feature_monitors`

requests.

This class thinly wraps an initial
[ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_monitors`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureMonitors`

requests and continue to iterate
through the `feature_monitors`

field on the
corresponding responses.

All the usual [ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsPager)

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

[ListFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesAsyncPager)

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

[ListFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesPager)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient -->

# Class MatchServiceClient (1.135.0)

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


MatchService is a Google managed service for efficient vector similarity search at scale.

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
`MatchServiceTransport` |
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

### MatchServiceClient

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MatchServiceTransport,Callable[..., MatchServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.match_service.FindNeighborsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.match_service.FindNeighborsResponse
```


Finds the nearest neighbors of each vector within the request.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_find_neighbors():
# Create a client
client = aiplatform_v1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.FindNeighbors. |
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
The response message for MatchService.FindNeighbors. |

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
`MatchServiceClient` |
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
`MatchServiceClient` |
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
`MatchServiceClient` |
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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

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

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1.types.match_service.ReadIndexDatapointsResponse
```


Reads the datapoints/vectors of the given IDs. A maximum of 1000 datapoints can be retrieved in a batch.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
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
The response message for MatchService.ReadIndexDatapoints. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricSpec -->

# Class PairwiseMetricSpec (1.135.0)

`PairwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`metric_prompt_template` |
`str`
Required. Metric prompt template for pairwise metric. This field is a member of `oneof` _ `_metric_prompt_template` .
|
`candidate_response_field_name` |
`str`
Optional. The field name of the candidate response. |
`baseline_response_field_name` |
`str`
Optional. The field name of the baseline response. |
`system_instruction` |
`str`
Optional. System instructions for pairwise metric. This field is a member of `oneof` _ `_system_instruction` .
|
`custom_output_format_config` |
Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwise_choice` and `explanation`
fields in the corresponding metric result will be empty.
|

## Methods

### PairwiseMetricSpec

`PairwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service -->

# Package featurestore_online_serving_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.featurestore_online_serving_service`

package.

## Classes

[FeaturestoreOnlineServingServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceAsyncClient)

A service for serving online feature values.

[FeaturestoreOnlineServingServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceClient)

A service for serving online feature values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest -->

# Class UpdateEndpointLongRunningRequest (1.135.0)

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

## Attribute |
|
|---|---|
Name |
Description |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the `client_connection_config` field, all the other fields'
update will be blocked.
|

## Methods

### UpdateEndpointLongRunningRequest

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexAiSearchConfig -->

# Class VertexAiSearchConfig (1.135.0)

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

## Attribute |
|
|---|---|
Name |
Description |
`serving_config` |
`str`
Vertex AI Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}`
or
`projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}` .
|

## Methods

### VertexAiSearchConfig

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest -->

# Class GetAnnotationSpecRequest (1.135.0)

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the AnnotationSpec resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/annotationSpecs/{annotation_spec}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetAnnotationSpecRequest

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighbors.Neighbor -->

# Class Neighbor (1.135.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
The id of the similar entity. |
`distance` |
`float`
The distance between the neighbor and the query vector. |
`entity_key_values` |
The attributes of the neighbor, e.g. filters, crowding and metadata Note that full entities are returned only when "return_full_entity" is set to true. Otherwise, only the "entity_id" and "distance" fields are populated. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeRequest -->

# Class StartNotebookRuntimeRequest (1.135.0)

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StartNotebookRuntimeRequest

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse -->

# Class ListModelEvaluationsResponse (1.135.0)

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

## Attributes |
|
|---|---|
Name |
Description |
`model_evaluations` |
`MutableSequence[`
List of ModelEvaluations in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelEvaluationsRequest.page_token to obtain that page. |

## Methods

### ListModelEvaluationsResponse

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse -->

# Class ListFeaturestoresResponse (1.135.0)

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

## Attributes |
|
|---|---|
Name |
Description |
`featurestores` |
`MutableSequence[`
The Featurestores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeaturestoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeaturestoresResponse

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest -->

# Class RebootPersistentResourceRequest (1.135.0)

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: `projects/{project_id_or_number}/locations/{location_id}/persistentResources/{persistent_resource_id}`
|

## Methods

### RebootPersistentResourceRequest

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagContexts -->

# Class RagContexts (1.135.0)

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

## Attribute |
|
|---|---|
Name |
Description |
`contexts` |
`MutableSequence[`
All its contexts. |

## Classes

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagContexts

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest -->

# Class RetrieveContextsRequest (1.135.0)

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`vertex_rag_store` |
The data source for Vertex RagStore. This field is a member of `oneof` _ `data_source` .
|
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`query` |
Required. Single RAG retrieve query. |

## Classes

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RetrieveContextsRequest

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardExperimentRequest -->

# Class DeleteTensorboardExperimentRequest (1.135.0)

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardExperiment to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### DeleteTensorboardExperimentRequest

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest -->

# Class UpdateExplanationDatasetRequest (1.135.0)

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The resource name of the Model to update. Format: `projects/{project}/locations/{location}/models/{model}`
|
`examples` |
The example config containing the location of the dataset. |

## Methods

### UpdateExplanationDatasetRequest

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob -->

# Class HyperparameterTuningJob (1.135.0)

```
HyperparameterTuningJob(
display_name: str,
custom_job: google.cloud.aiplatform.jobs.CustomJob,
metric_spec: typing.Dict[str, str],
parameter_spec: typing.Dict[
str, google.cloud.aiplatform.hyperparameter_tuning._ParameterSpec
],
max_trial_count: int,
parallel_trial_count: int,
max_failed_trial_count: int = 0,
search_algorithm: typing.Optional[str] = None,
measurement_selection: typing.Optional[str] = "best",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
)
```


Vertex AI Hyperparameter Tuning Job.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Time when the Job resource entered the `JOB_STATE_SUCCEEDED`

,
`JOB_STATE_FAILED`

, or `JOB_STATE_CANCELLED`

state.

### error

Detailed error info for this Job resource. Only populated when the
Job's state is `JOB_STATE_FAILED`

or `JOB_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
HyperparameterTuningJob should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the HyperparameterTuningJob is not peered with any network.

### preview

Exposes features available in preview for this class.

### resource_name

Full qualified resource name.

### start_time

Time when the Job resource entered the `JOB_STATE_RUNNING`

for the
first time.

### state

Fetch Job again and return the current JobState.

Returns |
|
|---|---|
Type |
Description |
`state (job_state.JobState)` |
Enum that describes the state of a Vertex AI job. |

### update_time

Time this resource was last updated.

### web_access_uris

Fetch the runnable job again and return the latest web access uris.

Returns |
|
|---|---|
Type |
Description |
`(Dict[str, Union[str, Dict[str, str]]])` |
Web access uris of the runnable job. |

## Methods

### HyperparameterTuningJob

```
HyperparameterTuningJob(
display_name: str,
custom_job: google.cloud.aiplatform.jobs.CustomJob,
metric_spec: typing.Dict[str, str],
parameter_spec: typing.Dict[
str, google.cloud.aiplatform.hyperparameter_tuning._ParameterSpec
],
max_trial_count: int,
parallel_trial_count: int,
max_failed_trial_count: int = 0,
search_algorithm: typing.Optional[str] = None,
measurement_selection: typing.Optional[str] = "best",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
)
```


Configures a HyperparameterTuning Job.

Example usage:

```
from google.cloud.aiplatform import hyperparameter_tuning as hpt
worker_pool_specs = [
{
"machine_spec": {
"machine_type": "n1-standard-4",
"accelerator_type": "NVIDIA_TESLA_K80",
"accelerator_count": 1,
},
"replica_count": 1,
"container_spec": {
"image_uri": container_image_uri,
"command": [],
"args": [],
},
}
]
custom_job = aiplatform.CustomJob(
display_name='my_job',
worker_pool_specs=worker_pool_specs,
labels={'my_key': 'my_value'},
)
hp_job = aiplatform.HyperparameterTuningJob(
display_name='hp-test',
custom_job=job,
metric_spec={
'loss': 'minimize',
},
parameter_spec={
'lr': hpt.DoubleParameterSpec(min=0.001, max=0.1, scale='log'),
'units': hpt.IntegerParameterSpec(min=4, max=128, scale='linear'),
'activation': hpt.CategoricalParameterSpec(values=['relu', 'selu']),
'batch_size': hpt.DiscreteParameterSpec(values=[128, 256], scale='linear')
},
max_trial_count=128,
parallel_trial_count=8,
labels={'my_key': 'my_value'},
)
hp_job.run()
print(hp_job.trials)
```


For more information on using hyperparameter tuning please visit:
[https://cloud.google.com/ai-platform-unified/docs/training/using-hyperparameter-tuning](https://cloud.google.com/ai-platform-unified/docs/training/using-hyperparameter-tuning)

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of the HyperparameterTuningJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`custom_job` |
`aiplatform.CustomJob`
Required. Configured CustomJob. The worker pool spec from this custom job applies to the CustomJobs created in all the trials. A persistent_resource_id can be specified on the custom job to be used when running this Hyperparameter Tuning job. |
`parameter_spec` |
`Dict[str, hyperparameter_tuning._ParameterSpec]`
Required. Dictionary representing parameters to optimize. The dictionary key is the metric_id, which is passed into your training job as a command line key word argument, and the dictionary value is the parameter specification of the metric. from google.cloud.aiplatform import hyperparameter_tuning as hpt parameter_spec={ 'decay': hpt.DoubleParameterSpec(min=1e-7, max=1, scale='linear'), 'learning_rate': hpt.DoubleParameterSpec(min=1e-7, max=1, scale='linear') 'batch_size': hpt.DiscreteParamterSpec(values=[4, 8, 16, 32, 64, 128], scale='linear') } Supported parameter specifications can be found until aiplatform.hyperparameter_tuning. These parameter specification are currently supported: DoubleParameterSpec, IntegerParameterSpec, CategoricalParameterSpace, DiscreteParameterSpec |
`max_trial_count` |
`int`
Required. The desired total number of Trials. |
`parallel_trial_count` |
`int`
Required. The desired number of Trials to run in parallel. |
`max_failed_trial_count` |
`int`
Optional. The number of failed Trials that need to be seen before failing the HyperparameterTuningJob. If set to 0, Vertex AI decides how many Trials must fail before the whole job fails. |
`search_algorithm` |
`str`
The search algorithm specified for the Study. Accepts one of the following: |
`measurement_selection` |
`str`
This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Accepts: 'best', 'last' Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose 'last'. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose 'best'. B) Are your measurements significantly noisy and/or irreproducible? If so, 'best' will tend to be over-optimistic, and it may be better to choose 'last'. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen. |
`project` |
`str`
Optional. Project to run the HyperparameterTuningjob in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run the HyperparameterTuning in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call HyperparameterTuning service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize HyperparameterTuningJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key options for a HyperparameterTuningJob. If this is set, then all resources created by the HyperparameterTuningJob will be encrypted with the provided encryption key. |

### cancel

`cancel() -> None`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

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
) -> google.cloud.aiplatform.jobs._RunnableJob
```


Get a Vertex AI Job for the given resource_name.

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
Optional. project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

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


List all instances of this Job Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

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

### run

```
run(
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
tensorboard: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
) -> None
```


Run this configured CustomJob.

Parameters |
|
|---|---|
Name |
Description |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`timeout` |
`int`
Optional. The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will unblock and it will be executed in a concurrent Future. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_completion

`wait_for_completion() -> None`


Waits for job to complete.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If job failed or cancelled. |

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until resource has been created.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient -->

# Class MatchServiceClient (1.135.0)

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


MatchService is a Google managed service for efficient vector similarity search at scale.

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
`MatchServiceTransport` |
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

### MatchServiceClient

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MatchServiceTransport,Callable[..., MatchServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsResponse
```


Finds the nearest neighbors of each vector within the request.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_find_neighbors():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.FindNeighbors. |
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
The response message for MatchService.FindNeighbors. |

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
`MatchServiceClient` |
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
`MatchServiceClient` |
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
`MatchServiceClient` |
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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

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

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsResponse
```


Reads the datapoints/vectors of the given IDs. A maximum of 1000 datapoints can be retrieved in a batch.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
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
The response message for MatchService.ReadIndexDatapoints. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse -->

# Class ListNotebookRuntimesResponse (1.135.0)

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtimes` |
`MutableSequence[`
List of NotebookRuntimes in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookRuntimesRequest.page_token to obtain that page. |

## Methods

### ListNotebookRuntimesResponse

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse -->

# Class ListModelMonitoringJobsResponse (1.135.0)

```
ListModelMonitoringJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.ListModelMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`model_monitoring_jobs` |
`MutableSequence[`
A list of ModelMonitoringJobs that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListModelMonitoringJobsResponse

```
ListModelMonitoringJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.ListModelMonitoringJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LineageSubgraph -->

# Class LineageSubgraph (1.135.0)

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
The Artifact nodes in the subgraph. |
`executions` |
`MutableSequence[`
The Execution nodes in the subgraph. |
`events` |
`MutableSequence[`
The Event edges between Artifacts and Executions in the subgraph. |

## Methods

### LineageSubgraph

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateReasoningEngineRequest -->

# Class CreateReasoningEngineRequest (1.135.0)

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the ReasoningEngine in. Format: `projects/{project}/locations/{location}`
|
`reasoning_engine` |
Required. The ReasoningEngine to create. |

## Methods

### CreateReasoningEngineRequest

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeOperationMetadata -->

# Class StartNotebookRuntimeOperationMetadata (1.135.0)

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### StartNotebookRuntimeOperationMetadata

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelGardenSource -->

# Class ModelGardenSource (1.135.0)

`ModelGardenSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Model Garden.

## Attributes |
|
|---|---|
Name |
Description |
`public_model_name` |
`str`
Required. The model garden source model resource name. |
`version_id` |
`str`
Optional. The model garden source model version ID. |
`skip_hf_model_cache` |
`bool`
Optional. Whether to avoid pulling the model from the HF cache. |

## Methods

### ModelGardenSource

`ModelGardenSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Model Garden.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service -->

# Package tensorboard_service (1.135.0)

API documentation for `aiplatform_v1.services.tensorboard_service`

package.

## Classes

[TensorboardServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceAsyncClient)

TensorboardService

[TensorboardServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient)

TensorboardService

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers)

API documentation for `aiplatform_v1.services.tensorboard_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelHyperparameterTuningJobRequest -->

# Class CancelHyperparameterTuningJobRequest (1.135.0)

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### CancelHyperparameterTuningJobRequest

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.OverlayType -->

# Class OverlayType (1.135.0)

`OverlayType(value)`


How the original image is displayed in the visualization.

## Enums |
|
|---|---|
Name |
Description |
`OVERLAY_TYPE_UNSPECIFIED` |
Default value. This is the same as NONE. |
`NONE` |
No overlay. |
`ORIGINAL` |
The attributions are shown on top of the original image. |
`GRAYSCALE` |
The attributions are shown on top of grayscaled version of the original image. |
`MASK_BLACK` |
The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

## Methods

### OverlayType

`OverlayType(value)`


How the original image is displayed in the visualization.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotationExplanation -->

# Class EvaluatedAnnotationExplanation (1.135.0)

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

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
`explanation` |
Explanation attribution response details. |

## Methods

### EvaluatedAnnotationExplanation

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest -->

# Class RetrieveContextsRequest (1.135.0)

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`vertex_rag_store` |
The data source for Vertex RagStore. This field is a member of `oneof` _ `data_source` .
|
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`query` |
Required. Single RAG retrieve query. |

## Classes

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RetrieveContextsRequest

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation -->

# Class CategoricalArrayTransformation (1.135.0)

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

## Methods

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAiSearchConfig -->

# Class VertexAiSearchConfig (1.135.0)

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

## Attribute |
|
|---|---|
Name |
Description |
`serving_config` |
`str`
Vertex AI Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}`
or
`projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}` .
|

## Methods

### VertexAiSearchConfig

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.GcsNotebookSource -->

# Class GcsNotebookSource (1.135.0)

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
|
`generation` |
`str`
The version of the Cloud Storage object to read. If unset, the current version of the object is read. See https://cloud.google.com/storage/docs/metadata#generation-number. |

## Methods

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ImageDataset -->

# Class ImageDataset (1.135.0)

```
ImageDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


A managed image dataset resource for Vertex AI.

Use this class to work with a managed image dataset. To create a managed image dataset, you need a datasource file in CSV format and a schema file in YAML format. A schema is optional for a custom model. You put the CSV file and the schema into Cloud Storage buckets.

Use image data for the following objectives:

- Single-label classification. For more information, see
[Prepare image training data for single-label classification](https://cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#single-label-classification). - Multi-label classification. For more information, see
[Prepare image training data for multi-label classification](https://cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#multi-label-classification). - Object detection. For more information, see
[Prepare image training data for object detection](https://cloud.google.com/vertex-ai/docs/image-data/object-detection/prepare-data).

The following code shows you how to create an image dataset by importing data from a CSV datasource file and a YAML schema file. The schema file you use depends on whether your image dataset is used for single-label classification, multi-label classification, or object detection.

```
my_dataset = aiplatform.ImageDataset.create(
display_name="my-image-dataset",
gcs_source=['gs://path/to/my/image-dataset.csv'],
import_schema_uri=['gs://path/to/my/schema.yaml']
)
```


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

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### ImageDataset

```
ImageDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
import_schema_uri: typing.Optional[str] = None,
data_item_labels: typing.Optional[typing.Dict] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.image_dataset.ImageDataset
```


Creates a new image dataset.

Optionally imports data into the dataset when a source and
`import_schema_uri`

are passed in.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
Optional. The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`import_schema_uri` |
`str`
Optional. A URI for a YAML file stored in Cloud Storage that describes the import schema used to validate the dataset. The schema is an |
`data_item_labels` |
`Dict`
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each image in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Images and documents are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
`project` |
`str`
Optional. The name of the Google Cloud project to which this |
`location` |
`str`
Optional. The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`image_dataset (ImageDataset)` |
An instantiated representation of the managed `ImageDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

```
import_data(
gcs_source: typing.Union[str, typing.Sequence[str]],
import_schema_uri: str,
data_item_labels: typing.Optional[typing.Dict] = None,
sync: bool = True,
import_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Upload data to existing managed dataset.

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

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


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient -->

# Class MatchServiceClient (1.134.0)

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


MatchService is a Google managed service for efficient vector similarity search at scale.

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
`MatchServiceTransport` |
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

### MatchServiceClient

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MatchServiceTransport,Callable[..., MatchServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsResponse
```


Finds the nearest neighbors of each vector within the request.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_find_neighbors():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.FindNeighbors. |
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
The response message for MatchService.FindNeighbors. |

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
`MatchServiceClient` |
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
`MatchServiceClient` |
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
`MatchServiceClient` |
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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

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

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsResponse
```


Reads the datapoints/vectors of the given IDs. A maximum of 1000 datapoints can be retrieved in a batch.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
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
The response message for MatchService.ReadIndexDatapoints. |

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob -->

# Class HyperparameterTuningJob (1.134.0)

```
HyperparameterTuningJob(
display_name: str,
custom_job: google.cloud.aiplatform.jobs.CustomJob,
metric_spec: typing.Dict[str, str],
parameter_spec: typing.Dict[
str, google.cloud.aiplatform.hyperparameter_tuning._ParameterSpec
],
max_trial_count: int,
parallel_trial_count: int,
max_failed_trial_count: int = 0,
search_algorithm: typing.Optional[str] = None,
measurement_selection: typing.Optional[str] = "best",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
)
```


Vertex AI Hyperparameter Tuning Job.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Time when the Job resource entered the `JOB_STATE_SUCCEEDED`

,
`JOB_STATE_FAILED`

, or `JOB_STATE_CANCELLED`

state.

### error

Detailed error info for this Job resource. Only populated when the
Job's state is `JOB_STATE_FAILED`

or `JOB_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
HyperparameterTuningJob should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the HyperparameterTuningJob is not peered with any network.

### preview

Exposes features available in preview for this class.

### resource_name

Full qualified resource name.

### start_time

Time when the Job resource entered the `JOB_STATE_RUNNING`

for the
first time.

### state

Fetch Job again and return the current JobState.

Returns |
|
|---|---|
Type |
Description |
`state (job_state.JobState)` |
Enum that describes the state of a Vertex AI job. |

### update_time

Time this resource was last updated.

### web_access_uris

Fetch the runnable job again and return the latest web access uris.

Returns |
|
|---|---|
Type |
Description |
`(Dict[str, Union[str, Dict[str, str]]])` |
Web access uris of the runnable job. |

## Methods

### HyperparameterTuningJob

```
HyperparameterTuningJob(
display_name: str,
custom_job: google.cloud.aiplatform.jobs.CustomJob,
metric_spec: typing.Dict[str, str],
parameter_spec: typing.Dict[
str, google.cloud.aiplatform.hyperparameter_tuning._ParameterSpec
],
max_trial_count: int,
parallel_trial_count: int,
max_failed_trial_count: int = 0,
search_algorithm: typing.Optional[str] = None,
measurement_selection: typing.Optional[str] = "best",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
)
```


Configures a HyperparameterTuning Job.

Example usage:

```
from google.cloud.aiplatform import hyperparameter_tuning as hpt
worker_pool_specs = [
{
"machine_spec": {
"machine_type": "n1-standard-4",
"accelerator_type": "NVIDIA_TESLA_K80",
"accelerator_count": 1,
},
"replica_count": 1,
"container_spec": {
"image_uri": container_image_uri,
"command": [],
"args": [],
},
}
]
custom_job = aiplatform.CustomJob(
display_name='my_job',
worker_pool_specs=worker_pool_specs,
labels={'my_key': 'my_value'},
)
hp_job = aiplatform.HyperparameterTuningJob(
display_name='hp-test',
custom_job=job,
metric_spec={
'loss': 'minimize',
},
parameter_spec={
'lr': hpt.DoubleParameterSpec(min=0.001, max=0.1, scale='log'),
'units': hpt.IntegerParameterSpec(min=4, max=128, scale='linear'),
'activation': hpt.CategoricalParameterSpec(values=['relu', 'selu']),
'batch_size': hpt.DiscreteParameterSpec(values=[128, 256], scale='linear')
},
max_trial_count=128,
parallel_trial_count=8,
labels={'my_key': 'my_value'},
)
hp_job.run()
print(hp_job.trials)
```


For more information on using hyperparameter tuning please visit:
[https://cloud.google.com/ai-platform-unified/docs/training/using-hyperparameter-tuning](https://cloud.google.com/ai-platform-unified/docs/training/using-hyperparameter-tuning)

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of the HyperparameterTuningJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`custom_job` |
`aiplatform.CustomJob`
Required. Configured CustomJob. The worker pool spec from this custom job applies to the CustomJobs created in all the trials. A persistent_resource_id can be specified on the custom job to be used when running this Hyperparameter Tuning job. |
`parameter_spec` |
`Dict[str, hyperparameter_tuning._ParameterSpec]`
Required. Dictionary representing parameters to optimize. The dictionary key is the metric_id, which is passed into your training job as a command line key word argument, and the dictionary value is the parameter specification of the metric. from google.cloud.aiplatform import hyperparameter_tuning as hpt parameter_spec={ 'decay': hpt.DoubleParameterSpec(min=1e-7, max=1, scale='linear'), 'learning_rate': hpt.DoubleParameterSpec(min=1e-7, max=1, scale='linear') 'batch_size': hpt.DiscreteParamterSpec(values=[4, 8, 16, 32, 64, 128], scale='linear') } Supported parameter specifications can be found until aiplatform.hyperparameter_tuning. These parameter specification are currently supported: DoubleParameterSpec, IntegerParameterSpec, CategoricalParameterSpace, DiscreteParameterSpec |
`max_trial_count` |
`int`
Required. The desired total number of Trials. |
`parallel_trial_count` |
`int`
Required. The desired number of Trials to run in parallel. |
`max_failed_trial_count` |
`int`
Optional. The number of failed Trials that need to be seen before failing the HyperparameterTuningJob. If set to 0, Vertex AI decides how many Trials must fail before the whole job fails. |
`search_algorithm` |
`str`
The search algorithm specified for the Study. Accepts one of the following: |
`measurement_selection` |
`str`
This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Accepts: 'best', 'last' Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose 'last'. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose 'best'. B) Are your measurements significantly noisy and/or irreproducible? If so, 'best' will tend to be over-optimistic, and it may be better to choose 'last'. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen. |
`project` |
`str`
Optional. Project to run the HyperparameterTuningjob in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run the HyperparameterTuning in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call HyperparameterTuning service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize HyperparameterTuningJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key options for a HyperparameterTuningJob. If this is set, then all resources created by the HyperparameterTuningJob will be encrypted with the provided encryption key. |

### cancel

`cancel() -> None`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

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
) -> google.cloud.aiplatform.jobs._RunnableJob
```


Get a Vertex AI Job for the given resource_name.

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
Optional. project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

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


List all instances of this Job Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

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

### run

```
run(
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
tensorboard: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
) -> None
```


Run this configured CustomJob.

Parameters |
|
|---|---|
Name |
Description |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`timeout` |
`int`
Optional. The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will unblock and it will be executed in a concurrent Future. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_completion

`wait_for_completion() -> None`


Waits for job to complete.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If job failed or cancelled. |

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until resource has been created.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ImageDataset -->

# Class ImageDataset (1.134.0)

```
ImageDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


A managed image dataset resource for Vertex AI.

Use this class to work with a managed image dataset. To create a managed image dataset, you need a datasource file in CSV format and a schema file in YAML format. A schema is optional for a custom model. You put the CSV file and the schema into Cloud Storage buckets.

Use image data for the following objectives:

- Single-label classification. For more information, see
[Prepare image training data for single-label classification](https://cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#single-label-classification). - Multi-label classification. For more information, see
[Prepare image training data for multi-label classification](https://cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#multi-label-classification). - Object detection. For more information, see
[Prepare image training data for object detection](https://cloud.google.com/vertex-ai/docs/image-data/object-detection/prepare-data).

The following code shows you how to create an image dataset by importing data from a CSV datasource file and a YAML schema file. The schema file you use depends on whether your image dataset is used for single-label classification, multi-label classification, or object detection.

```
my_dataset = aiplatform.ImageDataset.create(
display_name="my-image-dataset",
gcs_source=['gs://path/to/my/image-dataset.csv'],
import_schema_uri=['gs://path/to/my/schema.yaml']
)
```


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

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### ImageDataset

```
ImageDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
import_schema_uri: typing.Optional[str] = None,
data_item_labels: typing.Optional[typing.Dict] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.image_dataset.ImageDataset
```


Creates a new image dataset.

Optionally imports data into the dataset when a source and
`import_schema_uri`

are passed in.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
Optional. The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`import_schema_uri` |
`str`
Optional. A URI for a YAML file stored in Cloud Storage that describes the import schema used to validate the dataset. The schema is an |
`data_item_labels` |
`Dict`
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each image in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Images and documents are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
`project` |
`str`
Optional. The name of the Google Cloud project to which this |
`location` |
`str`
Optional. The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`image_dataset (ImageDataset)` |
An instantiated representation of the managed `ImageDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

```
import_data(
gcs_source: typing.Union[str, typing.Sequence[str]],
import_schema_uri: str,
data_item_labels: typing.Optional[typing.Dict] = None,
sync: bool = True,
import_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Upload data to existing managed dataset.

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

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


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation -->

# Class CategoricalArrayTransformation (1.134.0)

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

## Methods

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAiSearchConfig -->

# Class VertexAiSearchConfig (1.134.0)

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

## Attribute |
|
|---|---|
Name |
Description |
`serving_config` |
`str`
Vertex AI Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}`
or
`projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}` .
|

## Methods

### VertexAiSearchConfig

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.GcsNotebookSource -->

# Class GcsNotebookSource (1.134.0)

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
|
`generation` |
`str`
The version of the Cloud Storage object to read. If unset, the current version of the object is read. See https://cloud.google.com/storage/docs/metadata#generation-number. |

## Methods

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointLongRunningRequest -->

# Class UpdateEndpointLongRunningRequest (1.134.0)

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

## Attribute |
|
|---|---|
Name |
Description |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the `client_connection_config` field, all the other fields'
update will be blocked.
|

## Methods

### UpdateEndpointLongRunningRequest

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreRequest -->

# Class UpdateExampleStoreRequest (1.134.0)

`UpdateExampleStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.UpdateExampleStore.

## Attributes |
|
|---|---|
Name |
Description |
`example_store` |
Required. The Example Store which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. Supported fields: :: * `display_name`
* `description`
|

## Methods

### UpdateExampleStoreRequest

`UpdateExampleStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.UpdateExampleStore.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateBatchPredictionJobRequest -->

# Class CreateBatchPredictionJobRequest (1.134.0)

```
CreateBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateBatchPredictionJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the BatchPredictionJob in. Format: `projects/{project}/locations/{location}`
|
`batch_prediction_job` |
Required. The BatchPredictionJob to create. |

## Methods

### CreateBatchPredictionJobRequest

```
CreateBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateBatchPredictionJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec.DeveloperConnectSource -->

# Class DeveloperConnectSource (1.134.0)

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

## Attribute |
|
|---|---|
Name |
Description |
`config` |
Required. The Developer Connect configuration that defines the specific repository, revision, and directory to use as the source code root. |

## Methods

### DeveloperConnectSource

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

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

### SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CachedContent -->

# Class CachedContent (1.134.0)

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

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
Timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Input only. The TTL for this resource. The expiration time is computed: now + TTL. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cached_content} |
`display_name` |
`str`
Optional. Immutable. The user-generated meaningful display name of the cached content. |
`model` |
`str`
Immutable. The name of the `Model` to use for cached
content. Currently, only the published Gemini base models
are supported, in form of
projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}
|
`system_instruction` |
Optional. Input only. Immutable. Developer set system instruction. Currently, text only |
`contents` |
`MutableSequence[`
Optional. Input only. Immutable. The content to cache |
`tools` |
`MutableSequence[`
Optional. Input only. Immutable. A list of `Tools` the
model may use to generate the next response
|
`tool_config` |
Optional. Input only. Immutable. Tool config. This config is shared for all tools |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Creation time of the cache entry. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. When the cache entry was last updated in UTC time. |
`usage_metadata` |
Output only. Metadata on the usage of the cached content. |
`encryption_spec` |
Input only. Immutable. Customer-managed encryption key spec for a `CachedContent` . If set, this `CachedContent` and
all its sub-resources will be secured by this key.
|

## Classes

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata on the usage of the cached content.

## Methods

### CachedContent

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse -->

# Class ListFeaturestoresResponse (1.134.0)

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

## Attributes |
|
|---|---|
Name |
Description |
`featurestores` |
`MutableSequence[`
The Featurestores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeaturestoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeaturestoresResponse

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAnomaly.TabularAnomaly -->

# Class TabularAnomaly (1.134.0)

`TabularAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular anomaly details.

## Attributes |
|
|---|---|
Name |
Description |
`anomaly_uri` |
`str`
Additional anomaly information. e.g. Google Cloud Storage uri. |
`summary` |
`str`
Overview of this anomaly. |
`anomaly` |
`google.protobuf.struct_pb2.Value`
Anomaly body. |
`trigger_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time the anomaly was triggered. |
`condition` |
The alert condition associated with this anomaly. |

## Methods

### TabularAnomaly

`TabularAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular anomaly details.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest -->

# Class StartNotebookRuntimeRequest (1.134.0)

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StartNotebookRuntimeRequest

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsResponse -->

# Class SuggestTrialsResponse (1.134.0)

`SuggestTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.SuggestTrials.

## Attributes |
|
|---|---|
Name |
Description |
`trials` |
`MutableSequence[`
A list of Trials. |
`study_state` |
The state of the Study. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time at which the operation was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time at which operation processing completed. |

## Methods

### SuggestTrialsResponse

`SuggestTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.SuggestTrials.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtraction -->

# Class AutoMlTextExtraction (1.134.0)

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service -->

# Package reasoning_engine_execution_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.reasoning_engine_execution_service`

package.

## Classes

[ReasoningEngineExecutionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient)

A service for executing queries on Reasoning Engine.

[ReasoningEngineExecutionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceClient)

A service for executing queries on Reasoning Engine.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardExperimentRequest -->

# Class DeleteTensorboardExperimentRequest (1.134.0)

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardExperiment to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### DeleteTensorboardExperimentRequest

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse -->

# Class ListNotebookRuntimesResponse (1.134.0)

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtimes` |
`MutableSequence[`
List of NotebookRuntimes in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookRuntimesRequest.page_token to obtain that page. |

## Methods

### ListNotebookRuntimesResponse

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureStatsAndAnomalySpec -->

# Class FeatureStatsAndAnomalySpec (1.134.0)

`FeatureStatsAndAnomalySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines how to select FeatureStatsAndAnomaly to be populated in response. If set, retrieves FeatureStatsAndAnomaly generated by FeatureMonitors based on this spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`latest_stats_count` |
`int`
Optional. If set, returns the most recent count of stats. Valid value is [0, 100]. If stats_time_range is set, return most recent count of stats within the stats_time_range. This field is a member of `oneof` _ `_latest_stats_count` .
|
`stats_time_range` |
`google.type.interval_pb2.Interval`
Optional. If set, return all stats generated between [start_time, end_time). If latest_stats_count is set, return the most recent count of stats within the stats_time_range. |

## Methods

### FeatureStatsAndAnomalySpec

`FeatureStatsAndAnomalySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines how to select FeatureStatsAndAnomaly to be populated in response. If set, retrieves FeatureStatsAndAnomaly generated by FeatureMonitors based on this spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponse -->

# Class FunctionResponse (1.134.0)

`FunctionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result output from a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function is used as context to the model. This should contain the result of a [FunctionCall] made based on model prediction.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id` .
|
`name` |
`str`
Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name]. |
`response` |
`google.protobuf.struct_pb2.Struct`
Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output. |
`parts` |
`MutableSequence[`
Optional. Ordered `Parts` that constitute a function
response. Parts may have different IANA MIME types.
|

## Methods

### FunctionResponse

`FunctionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result output from a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function is used as context to the model. This should contain the result of a [FunctionCall] made based on model prediction.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.schedule_service.pagers`

module.

## Classes

[ListSchedulesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesAsyncPager)

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

[ListSchedulesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesPager)

```
ListSchedulesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse) object, and
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

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDataset -->

# Class TimeSeriesDataset (1.134.0)

```
TimeSeriesDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


A managed time series dataset resource for Vertex AI.

Use this class to work with time series datasets. A time series is a dataset
that contains data recorded at different time intervals. The dataset
includes time and at least one variable that's dependent on time. You use a
time series dataset for forecasting predictions. For more information, see
[Forecasting overview](https://cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview).

You can create a managed time series dataset from CSV files in a Cloud Storage bucket or from a BigQuery table.

The following code shows you how to create a `TimeSeriesDataset`

with a CSV
file that has the time series dataset:

```
my_dataset = aiplatform.TimeSeriesDataset.create(
display_name="my-dataset",
gcs_source=['gs://path/to/my/dataset.csv'],
)
```


The following code shows you how to create with a `TimeSeriesDataset`

with a
BigQuery table file that has the time series dataset:

```
my_dataset = aiplatform.TimeSeriesDataset.create(
display_name="my-dataset",
bq_source=['bq://path/to/my/bigquerydataset.train'],
)
```


## Properties

### column_names

Retrieve the columns for the dataset by extracting it from the Google Cloud Storage or Google BigQuery source.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
When no valid source is found. |

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

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### TimeSeriesDataset

```
TimeSeriesDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bq_source: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset
```


Creates a new time series dataset.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`bq_source` |
`str`
A BigQuery URI for the input table. For example, |
`project` |
`str`
The name of the Google Cloud project to which this |
`location` |
`str`
The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`time_series_dataset (TimeSeriesDataset)` |
An instantiated representation of the managed `TimeSeriesDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

`import_data()`


Upload data to existing managed dataset.

Parameters |
|
|---|---|
Name |
Description |
`gcs_source` |
`Union[str, Sequence[str]]`
Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see |
`import_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an |
`data_item_labels` |
`Dict`
Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`import_request_timeout` |
`float`
Optional. The timeout for the import request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

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


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CachedContent -->

# Class CachedContent (1.134.0)

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

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
Timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Input only. The TTL for this resource. The expiration time is computed: now + TTL. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cached_content} |
`display_name` |
`str`
Optional. Immutable. The user-generated meaningful display name of the cached content. |
`model` |
`str`
Immutable. The name of the `Model` to use for cached
content. Currently, only the published Gemini base models
are supported, in form of
projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}
|
`system_instruction` |
Optional. Input only. Immutable. Developer set system instruction. Currently, text only |
`contents` |
`MutableSequence[`
Optional. Input only. Immutable. The content to cache |
`tools` |
`MutableSequence[`
Optional. Input only. Immutable. A list of `Tools` the
model may use to generate the next response
|
`tool_config` |
Optional. Input only. Immutable. Tool config. This config is shared for all tools |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Creation time of the cache entry. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. When the cache entry was last updated in UTC time. |
`usage_metadata` |
Output only. Metadata on the usage of the cached content. |
`encryption_spec` |
Input only. Immutable. Customer-managed encryption key spec for a `CachedContent` . If set, this `CachedContent` and
all its sub-resources will be secured by this key.
|

## Classes

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata on the usage of the cached content.

## Methods

### CachedContent

`CachedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.endpoint_service.pagers`

module.

## Classes

[ListEndpointsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager)

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

[ListEndpointsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsPager)

```
ListEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse) object, and
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

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DedicatedResources -->

# Class DedicatedResources (1.134.0)

`DedicatedResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that are dedicated to a DeployedModel, and that need a higher degree of manual configuration.

## Attributes |
|
|---|---|
Name |
Description |
`machine_spec` |
Required. Immutable. The specification of a single machine used by the prediction. |
`min_replica_count` |
`int`
Required. Immutable. The minimum number of machine replicas this DeployedModel will be always deployed on. This value must be greater than or equal to 1. If traffic against the DeployedModel increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Immutable. The maximum number of replicas this DeployedModel may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the DeployedModel increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, will use min_replica_count as the default value. The value of this field impacts the charge against Vertex CPU and GPU quotas. Specifically, you will be charged for (max_replica_count \* number of cores in the selected machine type) and (max_replica_count \* number of GPUs per replica in the selected machine type). |
`required_replica_count` |
`int`
Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial model deployment/mutation is desired. If set, the model deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. If not set, the default required_replica_count will be min_replica_count. |
`autoscaling_metric_specs` |
`MutableSequence[`
Immutable. The metric specifications that overrides a resource utilization metric (CPU utilization, accelerator's duty cycle, and so on) target value (default to 60 if not set). At most one entry is allowed per metric. If machine_spec.accelerator_count is above 0, the autoscaling will be based on both CPU utilization and accelerator's duty cycle metrics and scale up when either metrics exceeds its target value while scale down if both metrics are under their target value. The default target value is 60 for both metrics. If machine_spec.accelerator_count is 0, the autoscaling will be based on CPU utilization metric only with default target value 60 if not explicitly set. For example, in the case of Online Prediction, if you want to override target CPU utilization to 80, you should set autoscaling_metric_specs.metric_name to `aiplatform.googleapis.com/prediction/online/cpu/utilization`
and
autoscaling_metric_specs.target
to `80` .
|
`spot` |
`bool`
Optional. If true, schedule the deployment workload on `spot VMs |

## Methods

### DedicatedResources

`DedicatedResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that are dedicated to a DeployedModel, and that need a higher degree of manual configuration.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentiment -->

# Class AutoMlTextSentiment (1.134.0)

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse -->

# Class FetchExamplesResponse (1.134.0)

`FetchExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.FetchExamples.

## Attributes |
|
|---|---|
Name |
Description |
`examples` |
`MutableSequence[`
The examples in the Example Store that satisfy the metadata filters. |
`next_page_token` |
`str`
A token, which can be sent as [FetchExamplesRequest.page_token][] to retrieve the next page. Absence of this field indicates there are no subsequent pages. |

## Methods

### FetchExamplesResponse

`FetchExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.FetchExamples.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelRequest -->

# Class UpdateModelRequest (1.134.0)

`UpdateModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UpdateModel.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
Required. The Model which replaces the resource on the server. When Model Versioning is enabled, the model.name will be used to determine whether to update the model or model version. 1. model.name with the @ value, e.g. models/123@1, refers to a version specific update. 2. model.name without the @ value, e.g. models/123, refers to a model update. 3. model.name with @-, e.g. models/123@-, refers to a model update. 4. Supported model fields: display_name, description; supported version-specific fields: version_description. Labels are supported in both scenarios. Both the model labels and the version labels are merged when a model is returned. When updating labels, if the request is for model-specific update, model label gets updated. Otherwise, version labels get updated. 5. A model name or model version name fields update mismatch will cause a precondition error. 6. One request cannot update both the model and the version fields. You must update them separately. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateModelRequest

`UpdateModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UpdateModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.job_service.pagers`

module.

## Classes

[ListBatchPredictionJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager)

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListBatchPredictionJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsPager)

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

[ListCustomJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsAsyncPager)

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

[ListCustomJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsPager)

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsAsyncPager)

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse) object, and
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

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsPager)

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

[ListHyperparameterTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager)

```
ListHyperparameterTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListHyperparameterTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsPager)

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsAsyncPager)

```
ListModelDeploymentMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager)

```
ListModelDeploymentMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsAsyncPager)

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsPager)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse) object, and
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

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasTrialDetailsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsAsyncPager)

```
ListNasTrialDetailsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
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
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse) object, and
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

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasTrialDetailsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsPager)

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

[SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchModelDeploymentMonitoringStatsAnomaliesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
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

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.memory_bank_service.pagers`

module.

## Classes

[ListMemoriesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesAsyncPager)

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

[ListMemoriesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesPager)

```
ListMemoriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


A pager for iterating through `list_memories`

requests.

This class thinly wraps an initial
[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse) object, and
provides an `__iter__`

method to iterate through its
`memories`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMemories`

requests and continue to iterate
through the `memories`

field on the
corresponding responses.

All the usual [ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeOperationMetadata -->

# Class StartNotebookRuntimeOperationMetadata (1.134.0)

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### StartNotebookRuntimeOperationMetadata

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse -->

# Class ListFeatureGroupsResponse (1.134.0)

`ListFeatureGroupsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureGroups.

## Attributes |
|
|---|---|
Name |
Description |
`feature_groups` |
`MutableSequence[`
The FeatureGroups matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureGroupsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureGroupsResponse

`ListFeatureGroupsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureGroups.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelGardenSource -->

# Class ModelGardenSource (1.134.0)

`ModelGardenSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Model Garden.

## Attributes |
|
|---|---|
Name |
Description |
`public_model_name` |
`str`
Required. The model garden source model resource name. |
`version_id` |
`str`
Optional. The model garden source model version ID. |
`skip_hf_model_cache` |
`bool`
Optional. Whether to avoid pulling the model from the HF cache. |

## Methods

### ModelGardenSource

`ModelGardenSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Model Garden.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

## Attribute |
|
|---|---|
Name |
Description |
`entity_id_selector` |
Required. Selectors choosing feature values of which entity id to be deleted from the EntityType. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig -->

# Class RagVectorDbConfig (1.134.0)

`RagVectorDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vector DB to use for RAG.

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
`rag_managed_db` |
The config for the RAG-managed Vector DB. This field is a member of `oneof` _ `vector_db` .
|
`weaviate` |
The config for the Weaviate. This field is a member of `oneof` _ `vector_db` .
|
`pinecone` |
The config for the Pinecone. This field is a member of `oneof` _ `vector_db` .
|
`vertex_feature_store` |
The config for the Vertex Feature Store. This field is a member of `oneof` _ `vector_db` .
|
`vertex_vector_search` |
The config for the Vertex Vector Search. This field is a member of `oneof` _ `vector_db` .
|
`rag_managed_vertex_vector_search` |
The config for the RAG-managed Vertex Vector Search 2.0. This field is a member of `oneof` _ `vector_db` .
|
`api_auth` |
Authentication config for the chosen Vector DB. |
`rag_embedding_model_config` |
Optional. Immutable. The embedding model config of the Vector DB. |

## Classes

### Pinecone

`Pinecone(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Pinecone.

### RagManagedDb

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RagManagedVertexVectorSearch

```
RagManagedVertexVectorSearch(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for the RAG-managed Vertex Vector Search 2.0.

### VertexFeatureStore

`VertexFeatureStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Feature Store.

### VertexVectorSearch

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

### Weaviate

`Weaviate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Weaviate.

## Methods

### RagVectorDbConfig

`RagVectorDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vector DB to use for RAG.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice -->

# Class ModelEvaluationSlice (1.134.0)

`ModelEvaluationSlice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the ModelEvaluationSlice. |
`slice_` |
Output only. The slice of the test data that is used to evaluate the Model. |
`metrics_schema_uri` |
`str`
Output only. Points to a YAML file stored on Google Cloud Storage describing the metrics of this ModelEvaluationSlice. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metrics` |
`google.protobuf.struct_pb2.Value`
Output only. Sliced evaluation metrics of the Model. The schema of the metrics is stored in metrics_schema_uri |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelEvaluationSlice was created. |
`model_explanation` |
Output only. Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for tabular Models. |

## Classes

### Slice

`Slice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Definition of a slice.

## Methods

### ModelEvaluationSlice

`ModelEvaluationSlice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata.RecordError.RecordErrorType -->

# Class RecordErrorType (1.134.0)

The size of the dense embedding vectors does not match with the specified dimension.

NAMESPACE_MISSING

The `namespace` field is missing.

PARSING_ERROR

Generic catch-all error. Only used for validation failure where the root cause cannot be easily retrieved programmatically.

DUPLICATE_NAMESPACE

There are multiple restricts with the same `namespace` value.

OP_IN_DATAPOINT

Numeric restrict has operator specified in datapoint.

MULTIPLE_VALUES

Numeric restrict has multiple values specified.

INVALID_NUMERIC_VALUE

Numeric restrict has invalid numeric value specified.

INVALID_ENCODING

File is not in UTF_8 format.

INVALID_SPARSE_DIMENSIONS

Error parsing sparse dimensions field.

INVALID_TOKEN_VALUE

Token restrict value is invalid.

INVALID_SPARSE_EMBEDDING

Invalid sparse embedding.

INVALID_EMBEDDING

Invalid dense embedding.

INVALID_EMBEDDING_METADATA

Invalid embedding metadata.

EMBEDDING_METADATA_EXCEEDS_SIZE_LIMIT

Embedding metadata exceeds size limit.

Methods

RecordErrorType

RecordErrorType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataRequest -->

# Class AssembleDataRequest (1.134.0)

`AssembleDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.AssembleData. Used only for MULTIMODAL datasets.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource (used only for MULTIMODAL datasets). Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`gemini_request_read_config` |
Optional. The read config for the dataset. |

## Methods

### AssembleDataRequest

`AssembleDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.AssembleData. Used only for MULTIMODAL datasets.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddExecutionEventsRequest -->

# Class AddExecutionEventsRequest (1.134.0)

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.

## Attributes |
|
|---|---|
Name |
Description |
`execution` |
`str`
Required. The resource name of the Execution that the Events connect Artifacts with. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`events` |
`MutableSequence[`
The Events to create and add. |

## Methods

### AddExecutionEventsRequest

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types -->

# Package params_v1beta1.types (1.134.0)

API documentation for `params_v1beta1.types`

package.

## Classes

[ImageClassificationPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageClassificationPredictionParams)

Prediction model parameters for Image Classification.

[ImageObjectDetectionPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageObjectDetectionPredictionParams)

Prediction model parameters for Image Object Detection.

[ImageSegmentationPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageSegmentationPredictionParams)

Prediction model parameters for Image Segmentation.

[VideoActionRecognitionPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoActionRecognitionPredictionParams)

Prediction model parameters for Video Action Recognition.

[VideoClassificationPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoClassificationPredictionParams)

Prediction model parameters for Video Classification.

[VideoObjectTrackingPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoObjectTrackingPredictionParams)

Prediction model parameters for Video Object Tracking.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.gen_ai_tuning_service.pagers`

module.

## Classes

[ListTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager)

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

[ListTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager)

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.pipeline_service.pagers`

module.

## Classes

[ListPipelineJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager)

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

[ListPipelineJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsPager)

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager)

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
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


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse) object, and
provides an `__aiter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TextDataset -->

# Class TextDataset (1.134.0)

```
TextDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


A managed text dataset resource for Vertex AI.

Use this class to work with a managed text dataset. To create a managed text dataset, you need a datasource file in CSV format and a schema file in YAML format. A schema is optional for a custom model. The CSV file and the schema are accessed in Cloud Storage buckets.

Use text data for the following objectives:

- Classification. For more information, see
[Prepare text training data for classification](https://cloud.google.com/vertex-ai/docs/text-data/classification/prepare-data). - Entity extraction. For more information, see
[Prepare text training data for entity extraction](https://cloud.google.com/vertex-ai/docs/text-data/entity-extraction/prepare-data). - Sentiment analysis. For more information, see [Prepare text training data for sentiment analysis](Prepare text training data for sentiment analysis).

The following code shows you how to create and import a text dataset with a CSV datasource file and a YAML schema file. The schema file you use depends on whether your text dataset is used for single-label classification, multi-label classification, or object detection.

```
my_dataset = aiplatform.TextDataset.create(
display_name="my-text-dataset",
gcs_source=['gs://path/to/my/text-dataset.csv'],
import_schema_uri=['gs://path/to/my/schema.yaml'],
)
```


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

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### TextDataset

```
TextDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
import_schema_uri: typing.Optional[str] = None,
data_item_labels: typing.Optional[typing.Dict] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.text_dataset.TextDataset
```


Creates a new text dataset.

Optionally imports data into this dataset when a source and
`import_schema_uri`

are passed in. The following is an example of how
this method is used:

```
ds = aiplatform.TextDataset.create(
display_name='my-dataset',
gcs_source='gs://my-bucket/dataset.csv',
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
Optional. The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`import_schema_uri` |
`str`
Optional. A URI for a YAML file stored in Cloud Storage that describes the import schema used to validate the dataset. The schema is an |
`data_item_labels` |
`Dict`
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each item in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Data items are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
`project` |
`str`
Optional. The name of the Google Cloud project to which this |
`location` |
`str`
Optional. The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`text_dataset (TextDataset)` |
An instantiated representation of the managed `TextDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

```
import_data(
gcs_source: typing.Union[str, typing.Sequence[str]],
import_schema_uri: str,
data_item_labels: typing.Optional[typing.Dict] = None,
sync: bool = True,
import_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Upload data to existing managed dataset.

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

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


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization.OverlayType -->

# Class OverlayType (1.134.0)

`OverlayType(value)`


How the original image is displayed in the visualization.

## Enums |
|
|---|---|
Name |
Description |
`OVERLAY_TYPE_UNSPECIFIED` |
Default value. This is the same as NONE. |
`NONE` |
No overlay. |
`ORIGINAL` |
The attributions are shown on top of the original image. |
`GRAYSCALE` |
The attributions are shown on top of grayscaled version of the original image. |
`MASK_BLACK` |
The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

## Methods

### OverlayType

`OverlayType(value)`


How the original image is displayed in the visualization.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe.GrpcAction -->

# Class GrpcAction (1.134.0)

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Port number of the gRPC service. Number must be in the range 1 to 65535. |
`service` |
`str`
Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md). If this is not specified, the default behavior is defined by gRPC. |

## Methods

### GrpcAction

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelRequest -->

# Class UpdateModelRequest (1.134.0)

`UpdateModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UpdateModel.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
Required. The Model which replaces the resource on the server. When Model Versioning is enabled, the model.name will be used to determine whether to update the model or model version. 1. model.name with the @ value, e.g. models/123@1, refers to a version specific update. 2. model.name without the @ value, e.g. models/123, refers to a model update. 3. model.name with @-, e.g. models/123@-, refers to a model update. 4. Supported model fields: display_name, description; supported version-specific fields: version_description. Labels are supported in both scenarios. Both the model labels and the version labels are merged when a model is returned. When updating labels, if the request is for model-specific update, model label gets updated. Otherwise, version labels get updated. 5. A model name or model version name fields update mismatch will cause a precondition error. 6. One request cannot update both the model and the version fields. You must update them separately. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateModelRequest

`UpdateModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UpdateModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateBatchPredictionJobRequest -->

# Class CreateBatchPredictionJobRequest (1.134.0)

```
CreateBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateBatchPredictionJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the BatchPredictionJob in. Format: `projects/{project}/locations/{location}`
|
`batch_prediction_job` |
Required. The BatchPredictionJob to create. |

## Methods

### CreateBatchPredictionJobRequest

```
CreateBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateBatchPredictionJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeOperationMetadata -->

# Class AssignNotebookRuntimeOperationMetadata (1.134.0)

```
AssignNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### AssignNotebookRuntimeOperationMetadata

```
AssignNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.AssignNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs.ModelType -->

# Class ModelType (1.134.0)

A Model best tailored to be used within Google Cloud, and which cannot be exported. Default.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

MOBILE_TF_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device with afterwards.

MOBILE_TF_HIGH_ACCURACY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.DeveloperConnectSource -->

# Class DeveloperConnectSource (1.134.0)

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

## Attribute |
|
|---|---|
Name |
Description |
`config` |
Required. The Developer Connect configuration that defines the specific repository, revision, and directory to use as the source code root. |

## Methods

### DeveloperConnectSource

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetVersionRequest -->

# Class GetDatasetVersionRequest (1.134.0)

`GetDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDatasetVersion.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetDatasetVersionRequest

`GetDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDatasetVersion.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointOperationMetadata -->

# Class CreateEndpointOperationMetadata (1.134.0)

```
CreateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.CreateEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployment_stage` |
Output only. The deployment stage of the model. Only populated if this CreateEndpoint request deploys a model at the same time. |

## Methods

### CreateEndpointOperationMetadata

```
CreateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.CreateEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse -->

# Class ListMetadataStoresResponse (1.134.0)

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_stores` |
`MutableSequence[`
The MetadataStores found for the Location. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataStoresRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataStoresResponse

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice -->

# Class ModelEvaluationSlice (1.134.0)

`ModelEvaluationSlice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the ModelEvaluationSlice. |
`slice_` |
Output only. The slice of the test data that is used to evaluate the Model. |
`metrics_schema_uri` |
`str`
Output only. Points to a YAML file stored on Google Cloud Storage describing the metrics of this ModelEvaluationSlice. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metrics` |
`google.protobuf.struct_pb2.Value`
Output only. Sliced evaluation metrics of the Model. The schema of the metrics is stored in metrics_schema_uri |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelEvaluationSlice was created. |
`model_explanation` |
Output only. Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for tabular Models. |

## Classes

### Slice

`Slice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Definition of a slice.

## Methods

### ModelEvaluationSlice

`ModelEvaluationSlice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamRawPredictRequest -->

# Class StreamRawPredictRequest (1.134.0)

`StreamRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamRawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. |

## Methods

### StreamRawPredictRequest

`StreamRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployIndexRequest -->

# Class UndeployIndexRequest (1.134.0)

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. |

## Methods

### UndeployIndexRequest

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteHyperparameterTuningJobRequest -->

# Class DeleteHyperparameterTuningJobRequest (1.134.0)

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource to be deleted. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### DeleteHyperparameterTuningJobRequest

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsResponse -->

# Class SuggestTrialsResponse (1.134.0)

`SuggestTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.SuggestTrials.

## Attributes |
|
|---|---|
Name |
Description |
`trials` |
`MutableSequence[`
A list of Trials. |
`study_state` |
The state of the Study. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time at which the operation was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time at which operation processing completed. |

## Methods

### SuggestTrialsResponse

`SuggestTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.SuggestTrials.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardTimeSeriesRequest -->

# Class GetTensorboardTimeSeriesRequest (1.134.0)

```
GetTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardTimeSeries resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### GetTensorboardTimeSeriesRequest

```
GetTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.Type -->

# Class Type (1.134.0)

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution].

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Should not be used. |
`PIXELS` |
Shows which pixel contributed to the image prediction. |
`OUTLINES` |
Shows which region contributed to the image prediction by outlining the region. |

## Methods

### Type

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution].

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoClassificationPredictionInstance -->

# Class VideoClassificationPredictionInstance (1.134.0)

```
VideoClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Classification.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoClassificationPredictionInstance

```
VideoClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Classification.

### VideoClassificationPredictionInstance

```
VideoClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Classification.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceResponse -->

# Class MigrateResourceResponse (1.134.0)

`MigrateResourceResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes a successfully migrated resource.

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
`dataset` |
`str`
Migrated Dataset's resource name. This field is a member of `oneof` _ `migrated_resource` .
|
`model` |
`str`
Migrated Model's resource name. This field is a member of `oneof` _ `migrated_resource` .
|
`migratable_resource` |
Before migration, the identifier in ml.googleapis.com, automl.googleapis.com or datalabeling.googleapis.com. |

## Methods

### MigrateResourceResponse

`MigrateResourceResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes a successfully migrated resource.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.DiscreteValueCondition -->

# Class DiscreteValueCondition (1.134.0)

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. Matches values of the parent parameter of 'DISCRETE' type. All values must exist in `discrete_value_spec` of parent parameter.
The Epsilon of the value matching is 1e-10.
|

## Methods

### DiscreteValueCondition

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SyntheticExample -->

# Class SyntheticExample (1.134.0)

`SyntheticExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single synthetic example, composed of multiple fields. Used for providing few-shot examples in the request and for returning generated examples in the response.

## Attribute |
|
|---|---|
Name |
Description |
`fields` |
`MutableSequence[`
Required. A list of fields that constitute an example. |

## Methods

### SyntheticExample

`SyntheticExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single synthetic example, composed of multiple fields. Used for providing few-shot examples in the request and for returning generated examples in the response.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

## Attribute |
|
|---|---|
Name |
Description |
`entity_id_selector` |
Required. Selectors choosing feature values of which entity id to be deleted from the EntityType. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse -->

# Class ListFeatureGroupsResponse (1.134.0)

`ListFeatureGroupsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureGroups.

## Attributes |
|
|---|---|
Name |
Description |
`feature_groups` |
`MutableSequence[`
The FeatureGroups matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureGroupsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureGroupsResponse

`ListFeatureGroupsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureGroups.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoObjectTrackingPredictionInstance -->

# Class VideoObjectTrackingPredictionInstance (1.134.0)

```
VideoObjectTrackingPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoObjectTrackingPredictionInstance

```
VideoObjectTrackingPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Object Tracking.

### VideoObjectTrackingPredictionInstance

```
VideoObjectTrackingPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddExecutionEventsRequest -->

# Class AddExecutionEventsRequest (1.134.0)

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.

## Attributes |
|
|---|---|
Name |
Description |
`execution` |
`str`
Required. The resource name of the Execution that the Events connect Artifacts with. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`events` |
`MutableSequence[`
The Events to create and add. |

## Methods

### AddExecutionEventsRequest

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse.PromptFeedback.BlockedReason -->

# Class BlockedReason (1.134.0)

`BlockedReason(value)`


Blocked reason enumeration.

## Enums |
|
|---|---|
Name |
Description |
`BLOCKED_REASON_UNSPECIFIED` |
Unspecified blocked reason. |
`SAFETY` |
Candidates blocked due to safety. |
`OTHER` |
Candidates blocked due to other reason. |
`BLOCKLIST` |
Candidates blocked due to the terms which are included from the terminology blocklist. |
`PROHIBITED_CONTENT` |
Candidates blocked due to prohibited content. |
`MODEL_ARMOR` |
The user prompt was blocked by Model Armor. |
`JAILBREAK` |
The user prompt was blocked due to jailbreak. |

## Methods

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SlackSource.SlackChannels.SlackChannel -->

# Class SlackChannel (1.134.0)

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

## Attributes |
|
|---|---|
Name |
Description |
`channel_id` |
`str`
Required. The Slack channel ID. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The starting timestamp for messages to import. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The ending timestamp for messages to import. |

## Methods

### SlackChannel

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse -->

# Class ListTrainingPipelinesResponse (1.134.0)

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines

## Attributes |
|
|---|---|
Name |
Description |
`training_pipelines` |
`MutableSequence[`
List of TrainingPipelines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTrainingPipelinesRequest.page_token to obtain that page. |

## Methods

### ListTrainingPipelinesResponse

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagRetrievalConfig -->

# Class RagRetrievalConfig (1.134.0)

`RagRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the context retrieval config.

## Attributes |
|
|---|---|
Name |
Description |
`top_k` |
`int`
Optional. The number of contexts to retrieve. |
`filter` |
Optional. Config for filters. |
`ranking` |
Optional. Config for ranking and reranking. |

## Classes

### Filter

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Ranking

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ranking and reranking.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagRetrievalConfig

`RagRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the context retrieval config.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceResponse -->

# Class MigrateResourceResponse (1.134.0)

`MigrateResourceResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes a successfully migrated resource.

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
`dataset` |
`str`
Migrated Dataset's resource name. This field is a member of `oneof` _ `migrated_resource` .
|
`model` |
`str`
Migrated Model's resource name. This field is a member of `oneof` _ `migrated_resource` .
|
`migratable_resource` |
Before migration, the identifier in ml.googleapis.com, automl.googleapis.com or datalabeling.googleapis.com. |

## Methods

### MigrateResourceResponse

`MigrateResourceResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes a successfully migrated resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagContexts.Context -->

# Class Context (1.134.0)

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`source_uri` |
`str`
If the file is imported from Cloud Storage or Google Drive, source_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source_uri will be file display name. |
`source_display_name` |
`str`
The file display name. |
`text` |
`str`
The text chunk. |
`score` |
`float`
According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type. For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is [0, 2], while 0 means the most relevant and 2 means the least relevant. This field is a member of `oneof` _ `_score` .
|
`chunk` |
Context of the retrieved chunk. |

## Methods

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse -->

# Class ListFeatureViewsResponse (1.134.0)

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

## Attributes |
|
|---|---|
Name |
Description |
`feature_views` |
`MutableSequence[`
The FeatureViews matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureViewsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureViewsResponse

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.VertexEndpointLogs -->

# Class VertexEndpointLogs (1.134.0)

`VertexEndpointLogs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Endpoint request response logging.

## Attribute |
|
|---|---|
Name |
Description |
`endpoints` |
`MutableSequence[str]`
List of endpoint resource names. The endpoints must enable the logging with the [Endpoint].[request_response_logging_config], and must contain the deployed model corresponding to the model version specified in [ModelMonitor].[model_monitoring_target]. |

## Methods

### VertexEndpointLogs

`VertexEndpointLogs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Endpoint request response logging.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs.ModelType -->

# Class ModelType (1.134.0)

A Model best tailored to be used within Google Cloud, and which cannot be exported. Default.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

MOBILE_TF_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device with afterwards.

MOBILE_TF_HIGH_ACCURACY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEntityTypeRequest -->

# Class UpdateEntityTypeRequest (1.134.0)

`UpdateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateEntityType.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
Required. The EntityType's `name` field is used to
identify the EntityType to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `description`
- `labels`
- `monitoring_config.snapshot_analysis.disabled`
- `monitoring_config.snapshot_analysis.monitoring_interval_days`
- `monitoring_config.snapshot_analysis.staleness_days`
- `monitoring_config.import_features_analysis.state`
- `monitoring_config.import_features_analysis.anomaly_detection_baseline`
- `monitoring_config.numerical_threshold_config.value`
- `monitoring_config.categorical_threshold_config.value`
- `offline_storage_ttl_days`
|

## Methods

### UpdateEntityTypeRequest

`UpdateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateEntityType.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service -->

# Package job_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.job_service`

package.

## Classes

[JobServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceAsyncClient)

A service for creating and managing Vertex AI's jobs.

[JobServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient)

A service for creating and managing Vertex AI's jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers)

API documentation for `aiplatform_v1beta1.services.job_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe.GrpcAction -->

# Class GrpcAction (1.134.0)

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Port number of the gRPC service. Number must be in the range 1 to 65535. |
`service` |
`str`
Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md). If this is not specified, the default behavior is defined by gRPC. |

## Methods

### GrpcAction

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient -->

# Class EvaluationServiceClient (1.134.0)

```
EvaluationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
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
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
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

### evaluate_dataset

```
evaluate_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateDatasetRequest,
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
) -> google.api_core.operation.Operation
```


Evaluates a dataset based on a set of given metrics.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_evaluate_dataset():
# Create a client
client = aiplatform_v1beta1.
```[EvaluationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[EvaluationDataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationDataset.html)()
dataset.gcs_source.uris = ['uris_value1', 'uris_value2']
output_config = aiplatform_v1beta1.[OutputConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputConfig.html)()
output_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[EvaluateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRequest.html)(
location="location_value",
dataset=dataset,
output_config=output_config,
)
# Make the request
operation = client.[evaluate_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html#google_cloud_aiplatform_v1beta1_services_evaluation_service_EvaluationServiceClient_evaluate_dataset)(request=request)
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
The request object. Request message for EvaluationService.EvaluateDataset. |
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

### evaluate_instances

```
evaluate_instances(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateInstancesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateInstancesResponse
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
from google.cloud import aiplatform_v1beta1
def sample_evaluate_instances():
# Create a client
client = aiplatform_v1beta1.
```[EvaluationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[EvaluateInstancesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateInstancesRequest.html)(
location="location_value",
)
# Make the request
response = client.[evaluate_instances](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html#google_cloud_aiplatform_v1beta1_services_evaluation_service_EvaluationServiceClient_evaluate_instances)(request=request)
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeOperationMetadata -->

# Class AssignNotebookRuntimeOperationMetadata (1.134.0)

```
AssignNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### AssignNotebookRuntimeOperationMetadata

```
AssignNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.AssignNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexRequest -->

# Class UndeployIndexRequest (1.134.0)

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. |

## Methods

### UndeployIndexRequest

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TunedModelCheckpoint -->

# Class TunedModelCheckpoint (1.134.0)

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |
`endpoint` |
`str`
The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .
|

## Methods

### TunedModelCheckpoint

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointOperationMetadata -->

# Class CreateEndpointOperationMetadata (1.134.0)

```
CreateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.CreateEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployment_stage` |
Output only. The deployment stage of the model. Only populated if this CreateEndpoint request deploys a model at the same time. |

## Methods

### CreateEndpointOperationMetadata

```
CreateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.CreateEndpoint.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureStatsAndAnomaly -->

# Class FeatureStatsAndAnomaly (1.134.0)

`FeatureStatsAndAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats and Anomaly generated by FeatureMonitorJobs. Anomaly only includes Drift.

## Attributes |
|
|---|---|
Name |
Description |
`feature_id` |
`str`
Feature Id. |
`feature_stats` |
`google.protobuf.struct_pb2.Value`
Feature stats. e.g. histogram buckets. In the format of tensorflow.metadata.v0.DatasetFeatureStatistics. |
`distribution_deviation` |
`float`
Deviation from the current stats to baseline stats. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. |
`drift_detection_threshold` |
`float`
This is the threshold used when detecting drifts, which is set in FeatureMonitor.FeatureSelectionConfig.FeatureConfig.drift_threshold |
`drift_detected` |
`bool`
If set to true, indicates current stats is detected as and comparing with baseline stats. |
`stats_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The timestamp we take snapshot for feature values to generate stats. |
`feature_monitor_job_id` |
`int`
The ID of the FeatureMonitorJob that generated this FeatureStatsAndAnomaly. |
`feature_monitor_id` |
`str`
The ID of the FeatureMonitor that this FeatureStatsAndAnomaly generated according to. |

## Methods

### FeatureStatsAndAnomaly

`FeatureStatsAndAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats and Anomaly generated by FeatureMonitorJobs. Anomaly only includes Drift.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Optimized -->

# Class Optimized (1.134.0)

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

## Methods

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs -->

# Class AutoMlTextExtractionInputs (1.134.0)

`AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteHyperparameterTuningJobRequest -->

# Class DeleteHyperparameterTuningJobRequest (1.134.0)

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource to be deleted. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### DeleteHyperparameterTuningJobRequest

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardTimeSeriesRequest -->

# Class GetTensorboardTimeSeriesRequest (1.134.0)

```
GetTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardTimeSeries resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### GetTensorboardTimeSeriesRequest

```
GetTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse -->

# Class ListMetadataStoresResponse (1.134.0)

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_stores` |
`MutableSequence[`
The MetadataStores found for the Location. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataStoresRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataStoresResponse

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtraction -->

# Class AutoMlTextExtraction (1.134.0)

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeOperationMetadata -->

# Class UpgradeNotebookRuntimeOperationMetadata (1.134.0)

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### UpgradeNotebookRuntimeOperationMetadata

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamRawPredictRequest -->

# Class StreamRawPredictRequest (1.134.0)

`StreamRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamRawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. |

## Methods

### StreamRawPredictRequest

`StreamRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamRawPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig.HybridSearchConfig -->

# Class HybridSearchConfig (1.134.0)

`HybridSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for hybrid search.

## Attributes |
|
|---|---|
Name |
Description |
`sparse_embedding_config` |
Optional. The configuration for sparse embedding generation. This field is optional the default behavior depends on the vector database choice on the RagCorpus. |
`dense_embedding_model_prediction_endpoint` |
Required. The Vertex AI Prediction Endpoint that hosts the embedding model for dense embedding generations. |

## Methods

### HybridSearchConfig

`HybridSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for hybrid search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoClassificationPredictionInstance -->

# Class VideoClassificationPredictionInstance (1.134.0)

```
VideoClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Classification.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoClassificationPredictionInstance

```
VideoClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Classification.

### VideoClassificationPredictionInstance

```
VideoClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Classification.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.DiscreteValueCondition -->

# Class DiscreteValueCondition (1.134.0)

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. Matches values of the parent parameter of 'DISCRETE' type. All values must exist in `discrete_value_spec` of parent parameter.
The Epsilon of the value matching is 1e-10.
|

## Methods

### DiscreteValueCondition

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FlexStart -->

# Class FlexStart (1.134.0)

`FlexStart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.

## Attribute |
|
|---|---|
Name |
Description |
`max_runtime_duration` |
`google.protobuf.duration_pb2.Duration`
The max duration of the deployment is max_runtime_duration. The deployment will be terminated after the duration. The max_runtime_duration can be set up to 7 days. |

## Methods

### FlexStart

`FlexStart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEntityTypeRequest -->

# Class UpdateEntityTypeRequest (1.134.0)

`UpdateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateEntityType.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
Required. The EntityType's `name` field is used to
identify the EntityType to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `description`
- `labels`
- `monitoring_config.snapshot_analysis.disabled`
- `monitoring_config.snapshot_analysis.monitoring_interval_days`
- `monitoring_config.snapshot_analysis.staleness_days`
- `monitoring_config.import_features_analysis.state`
- `monitoring_config.import_features_analysis.anomaly_detection_baseline`
- `monitoring_config.numerical_threshold_config.value`
- `monitoring_config.categorical_threshold_config.value`
- `offline_storage_ttl_days`
|

## Methods

### UpdateEntityTypeRequest

`UpdateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateEntityType.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexRagStore -->

# Class VertexRagStore (1.134.0)

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex RAG Store for grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_resources` |
`MutableSequence[`
Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support. |
`similarity_top_k` |
`int`
Optional. Number of top k results to return from the selected corpora. This field is a member of `oneof` _ `_similarity_top_k` .
|
`vector_distance_threshold` |
`float`
Optional. Only return results with vector distance smaller than the threshold. This field is a member of `oneof` _ `_vector_distance_threshold` .
|
`rag_retrieval_config` |
Optional. The retrieval config for the Rag query. |

## Classes

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Methods

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex RAG Store for grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ImageObjectDetectionPredictionResult -->

# Class ImageObjectDetectionPredictionResult (1.134.0)

```
ImageObjectDetectionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Object Detection.

## Attributes |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[int]`
The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly. |
`display_names` |
`MutableSequence[str]`
The display names of the AnnotationSpecs that had been identified, order matches the IDs. |
`confidences` |
`MutableSequence[float]`
The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids. |
`bboxes` |
`MutableSequence[google.protobuf.struct_pb2.ListValue]`
Bounding boxes, i.e. the rectangles over the image, that pinpoint the found AnnotationSpecs. Given in order that matches the IDs. Each bounding box is an array of 4 numbers `xMin` , `xMax` , `yMin` , and `yMax` , which represent
the extremal coordinates of the box. They are relative to
the image size, and the point 0,0 is in the top left of the
image.
|

## Methods

### ImageObjectDetectionPredictionResult

```
ImageObjectDetectionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Object Detection.

### ImageObjectDetectionPredictionResult

```
ImageObjectDetectionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Object Detection.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigRequest -->

# Class SetPublisherModelConfigRequest (1.134.0)

```
SetPublisherModelConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.SetPublisherModelConfig.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the publisher model, in the format of `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` .
|
`publisher_model_config` |
Required. The publisher model config. |

## Methods

### SetPublisherModelConfigRequest

```
SetPublisherModelConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.SetPublisherModelConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Citation -->

# Class Citation (1.134.0)

`Citation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source attributions for content.

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Output only. Start index into the content. |
`end_index` |
`int`
Output only. End index into the content. |
`uri` |
`str`
Output only. Url reference of the attribution. |
`title` |
`str`
Output only. Title of the attribution. |
`license_` |
`str`
Output only. License of the attribution. |
`publication_date` |
`google.type.date_pb2.Date`
Output only. Publication date of the attribution. |

## Methods

### Citation

`Citation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source attributions for content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.ResourceReference -->

# Class ResourceReference (1.134.0)

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

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
`uri` |
`str`
The URI of the resource. This field is a member of `oneof` _ `reference` .
|
`resource_name` |
`str`
The resource name of the Google Cloud resource. This field is a member of `oneof` _ `reference` .
|
`use_case` |
`str`
Use case (CUJ) of the resource. This field is a member of `oneof` _ `reference` .
|
`description` |
`str`
Description of the resource. This field is a member of `oneof` _ `reference` .
|

## Methods

### ResourceReference

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse -->

# Class ListReasoningEnginesResponse (1.134.0)

```
ListReasoningEnginesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ReasoningEngineService.ListReasoningEngines

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engines` |
`MutableSequence[`
List of ReasoningEngines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListReasoningEnginesRequest.page_token to obtain that page. |

## Methods

### ListReasoningEnginesResponse

```
ListReasoningEnginesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ReasoningEngineService.ListReasoningEngines

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service -->

# Package model_service (1.134.0)

API documentation for `aiplatform_v1.services.model_service`

package.

## Classes

[ModelServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient)

A service for managing Vertex AI's machine learning Models.

[ModelServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceClient)

A service for managing Vertex AI's machine learning Models.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers)

API documentation for `aiplatform_v1.services.model_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoObjectTrackingPredictionInstance -->

# Class VideoObjectTrackingPredictionInstance (1.134.0)

```
VideoObjectTrackingPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoObjectTrackingPredictionInstance

```
VideoObjectTrackingPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Object Tracking.

### VideoObjectTrackingPredictionInstance

```
VideoObjectTrackingPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse -->

# Class ListTrainingPipelinesResponse (1.134.0)

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines

## Attributes |
|
|---|---|
Name |
Description |
`training_pipelines` |
`MutableSequence[`
List of TrainingPipelines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTrainingPipelinesRequest.page_token to obtain that page. |

## Methods

### ListTrainingPipelinesResponse

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SlackSource.SlackChannels.SlackChannel -->

# Class SlackChannel (1.134.0)

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

## Attributes |
|
|---|---|
Name |
Description |
`channel_id` |
`str`
Required. The Slack channel ID. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The starting timestamp for messages to import. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The ending timestamp for messages to import. |

## Methods

### SlackChannel

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexEndpointRequest -->

# Class UpdateIndexEndpointRequest (1.134.0)

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexEndpointRequest

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitoringJobRequest -->

# Class DeleteModelMonitoringJobRequest (1.134.0)

```
DeleteModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.DeleteModelMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}/modelMonitoringJobs/{model_monitoring_job}`
|

## Methods

### DeleteModelMonitoringJobRequest

```
DeleteModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.DeleteModelMonitoringJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse -->

# Class ListFeatureViewsResponse (1.134.0)

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

## Attributes |
|
|---|---|
Name |
Description |
`feature_views` |
`MutableSequence[`
The FeatureViews matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureViewsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureViewsResponse

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LustreMount -->

# Class LustreMount (1.134.0)

`LustreMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Lustre file system.

## Attributes |
|
|---|---|
Name |
Description |
`instance_ip` |
`str`
Required. IP address of the Lustre instance. |
`volume_handle` |
`str`
Required. The unique identifier of the Lustre volume. |
`filesystem` |
`str`
Required. The name of the Lustre filesystem. |
`mount_point` |
`str`
Required. Destination mount path. The Lustre file system will be mounted for the user under /mnt/lustre/ |

## Methods

### LustreMount

`LustreMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Lustre file system.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.BaseModelSource -->

# Class BaseModelSource (1.134.0)

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

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
`model_garden_source` |
Source information of Model Garden models. This field is a member of `oneof` _ `source` .
|
`genie_source` |
Information about the base model of Genie models. This field is a member of `oneof` _ `source` .
|

## Methods

### BaseModelSource

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataConfig.ExportUse -->

# Class ExportUse (1.134.0)

`ExportUse(value)`


ExportUse indicates the usage of the exported files. It restricts file destination, format, annotations to be exported, whether to allow unannotated data to be exported and whether to clone files to temp Cloud Storage bucket.

## Enums |
|
|---|---|
Name |
Description |
`EXPORT_USE_UNSPECIFIED` |
Regular user export. |
`CUSTOM_CODE_TRAINING` |
Export for custom code training. |

## Methods

### ExportUse

`ExportUse(value)`


ExportUse indicates the usage of the exported files. It restricts file destination, format, annotations to be exported, whether to allow unannotated data to be exported and whether to clone files to temp Cloud Storage bucket.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelEulaAcceptance -->

# Class PublisherModelEulaAcceptance (1.134.0)

```
PublisherModelEulaAcceptance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ModelGardenService.UpdatePublisherModelEula][].

## Attributes |
|
|---|---|
Name |
Description |
`project_number` |
`int`
The project number requesting access for named model. |
`publisher_model` |
`str`
The publisher model resource name. |
`publisher_model_eula_acked` |
`bool`
The EULA content acceptance status. |

## Methods

### PublisherModelEulaAcceptance

```
PublisherModelEulaAcceptance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ModelGardenService.UpdatePublisherModelEula][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec.FeatureAttributionSpec -->

# Class FeatureAttributionSpec (1.134.0)

`FeatureAttributionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature attribution monitoring spec.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[str]`
Feature names interested in monitoring. These should be a subset of the input feature names specified in the monitoring schema. If the field is not specified all features outlied in the monitoring schema will be used. |
`default_alert_condition` |
Default alert condition for all the features. |
`feature_alert_conditions` |
`MutableMapping[str, `
Per feature alert condition will override default alert condition. |
`batch_explanation_dedicated_resources` |
The config of resources used by the Model Monitoring during the batch explanation for non-AutoML models. If not set, `n1-standard-2` machine type will be used by default.
|

## Classes

### FeatureAlertConditionsEntry

`FeatureAlertConditionsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### FeatureAttributionSpec

`FeatureAttributionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature attribution monitoring spec.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiRequestReadConfig -->

# Class GeminiRequestReadConfig (1.134.0)

`GeminiRequestReadConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to read Gemini requests from a multimodal dataset.

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
`template_config` |
Gemini request template with placeholders. This field is a member of `oneof` _ `read_config` .
|
`assembled_request_column_name` |
`str`
Optional. Column name in the dataset table that contains already fully assembled Gemini requests. This field is a member of `oneof` _ `read_config` .
|

## Methods

### GeminiRequestReadConfig

`GeminiRequestReadConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to read Gemini requests from a multimodal dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.MetricSpec -->

# Class MetricSpec (1.134.0)

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`metric_id` |
`str`
Required. The ID of the metric. Must not contain whitespaces and must be unique amongst all MetricSpecs. |
`goal` |
Required. The optimization goal of the metric. |
`safety_config` |
Used for safe search. In the case, the metric will be a safety metric. You must provide a separate metric for objective metric. This field is a member of `oneof` _ `_safety_config` .
|

## Classes

### GoalType

`GoalType(value)`


The available types of optimization goals.

### SafetyMetricConfig

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ChatCompletionsRequest -->

# Class ChatCompletionsRequest (1.134.0)

`ChatCompletionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.ChatCompletions]

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
Optional. The prediction input. Supports HTTP headers and arbitrary data payload. |

## Methods

### ChatCompletionsRequest

`ChatCompletionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.ChatCompletions]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelCheckpoint -->

# Class TunedModelCheckpoint (1.134.0)

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |
`endpoint` |
`str`
The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .
|

## Methods

### TunedModelCheckpoint

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.ResourceReference -->

# Class ResourceReference (1.134.0)

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

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
`uri` |
`str`
The URI of the resource. This field is a member of `oneof` _ `reference` .
|
`resource_name` |
`str`
The resource name of the Google Cloud resource. This field is a member of `oneof` _ `reference` .
|
`use_case` |
`str`
Use case (CUJ) of the resource. This field is a member of `oneof` _ `reference` .
|
`description` |
`str`
Description of the resource. This field is a member of `oneof` _ `reference` .
|

## Methods

### ResourceReference

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse -->

# Class ListTensorboardRunsResponse (1.134.0)

`ListTensorboardRunsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_runs` |
`MutableSequence[`
The TensorboardRuns mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardRunsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardRunsResponse

`ListTensorboardRunsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboardRuns.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial.State -->

# Class State (1.134.0)

`State(value)`


Describes a Trial state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The Trial state is unspecified. |
`REQUESTED` |
Indicates that a specific Trial has been requested, but it has not yet been suggested by the service. |
`ACTIVE` |
Indicates that the Trial has been suggested. |
`STOPPING` |
Indicates that the Trial should stop according to the service. |
`SUCCEEDED` |
Indicates that the Trial is completed successfully. |
`INFEASIBLE` |
Indicates that the Trial should not be attempted again. The service will set a Trial to INFEASIBLE when it's done but missing the final_measurement. |

## Methods

### State

`State(value)`


Describes a Trial state.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsResponse.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`datapoint` |
The datapoint of the neighbor. Note that full datapoints are returned only when "return_full_datapoint" is set to true. Otherwise, only the "datapoint_id" and "crowding_tag" fields are populated. |
`distance` |
`float`
The distance between the neighbor and the dense embedding query. |
`sparse_distance` |
`float`
The distance between the neighbor and the query sparse_embedding. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PostStartupScriptConfig.PostStartupScriptBehavior -->

# Class PostStartupScriptBehavior (1.134.0)

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post-startup script behavior.

## Enums |
|
|---|---|
Name |
Description |
`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` |
Unspecified post-startup script behavior. |
`RUN_ONCE` |
Run the post-startup script only once, during runtime creation. |
`RUN_EVERY_START` |
Run the post-startup script after every start. |
`DOWNLOAD_AND_RUN_EVERY_START` |
After every start, download the post-startup script from its source and run it. |

## Methods

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post-startup script behavior.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeTemplateRequest -->

# Class DeleteNotebookRuntimeTemplateRequest (1.134.0)

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### DeleteNotebookRuntimeTemplateRequest

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeOperationMetadata -->

# Class UpgradeNotebookRuntimeOperationMetadata (1.134.0)

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### UpgradeNotebookRuntimeOperationMetadata

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.BaseModelSource -->

# Class BaseModelSource (1.134.0)

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

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
`model_garden_source` |
Source information of Model Garden models. This field is a member of `oneof` _ `source` .
|
`genie_source` |
Information about the base model of Genie models. This field is a member of `oneof` _ `source` .
|

## Methods

### BaseModelSource

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient -->

# Class MatchServiceAsyncClient (1.134.0)

```
MatchServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


MatchService is a Google managed service for efficient vector similarity search at scale.

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
`MatchServiceTransport` |
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

### MatchServiceAsyncClient

```
MatchServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MatchServiceTransport,Callable[..., MatchServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.match_service.FindNeighborsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.match_service.FindNeighborsResponse
```


Finds the nearest neighbors of each vector within the request.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_find_neighbors():
# Create a client
client = aiplatform_v1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceAsyncClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.FindNeighbors. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
The response message for MatchService.FindNeighbors. |

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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport
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

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1.types.match_service.ReadIndexDatapointsResponse
```


Reads the datapoints/vectors of the given IDs. A maximum of 1000 datapoints can be retrieved in a batch.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceAsyncClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
The response message for MatchService.ReadIndexDatapoints. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextExtractionPredictionResult -->

# Class TextExtractionPredictionResult (1.134.0)

```
TextExtractionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Extraction.

## Attributes |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[int]`
The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly. |
`display_names` |
`MutableSequence[str]`
The display names of the AnnotationSpecs that had been identified, order matches the IDs. |
`text_segment_start_offsets` |
`MutableSequence[int]`
The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet. |
`text_segment_end_offsets` |
`MutableSequence[int]`
The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet. |
`confidences` |
`MutableSequence[float]`
The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids. |

## Methods

### TextExtractionPredictionResult

```
TextExtractionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Extraction.

### TextExtractionPredictionResult

```
TextExtractionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Extraction.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Citation -->

# Class Citation (1.134.0)

`Citation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source attributions for content.

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Output only. Start index into the content. |
`end_index` |
`int`
Output only. End index into the content. |
`uri` |
`str`
Output only. Url reference of the attribution. |
`title` |
`str`
Output only. Title of the attribution. |
`license_` |
`str`
Output only. License of the attribution. |
`publication_date` |
`google.type.date_pb2.Date`
Output only. Publication date of the attribution. |

## Methods

### Citation

`Citation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source attributions for content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse -->

# Class ListReasoningEnginesResponse (1.134.0)

```
ListReasoningEnginesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ReasoningEngineService.ListReasoningEngines

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engines` |
`MutableSequence[`
List of ReasoningEngines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListReasoningEnginesRequest.page_token to obtain that page. |

## Methods

### ListReasoningEnginesResponse

```
ListReasoningEnginesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ReasoningEngineService.ListReasoningEngines

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageObjectDetectionPredictionResult -->

# Class ImageObjectDetectionPredictionResult (1.134.0)

```
ImageObjectDetectionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Object Detection.

## Attributes |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[int]`
The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly. |
`display_names` |
`MutableSequence[str]`
The display names of the AnnotationSpecs that had been identified, order matches the IDs. |
`confidences` |
`MutableSequence[float]`
The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids. |
`bboxes` |
`MutableSequence[google.protobuf.struct_pb2.ListValue]`
Bounding boxes, i.e. the rectangles over the image, that pinpoint the found AnnotationSpecs. Given in order that matches the IDs. Each bounding box is an array of 4 numbers `xMin` , `xMax` , `yMin` , and `yMax` , which represent
the extremal coordinates of the box. They are relative to
the image size, and the point 0,0 is in the top left of the
image.
|

## Methods

### ImageObjectDetectionPredictionResult

```
ImageObjectDetectionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Object Detection.

### ImageObjectDetectionPredictionResult

```
ImageObjectDetectionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Object Detection.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.MetricSpec -->

# Class MetricSpec (1.134.0)

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`metric_id` |
`str`
Required. The ID of the metric. Must not contain whitespaces and must be unique amongst all MetricSpecs. |
`goal` |
Required. The optimization goal of the metric. |
`safety_config` |
Used for safe search. In the case, the metric will be a safety metric. You must provide a separate metric for objective metric. This field is a member of `oneof` _ `_safety_config` .
|

## Classes

### GoalType

`GoalType(value)`


The available types of optimization goals.

### SafetyMetricConfig

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Retrieval -->

# Class Retrieval (1.134.0)

`Retrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a retrieval tool that model can call to access external knowledge.

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
`vertex_ai_search` |
Set to use data source powered by Vertex AI Search. This field is a member of `oneof` _ `source` .
|
`vertex_rag_store` |
Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService. This field is a member of `oneof` _ `source` .
|
`disable_attribution` |
`bool`
Optional. Deprecated. This option is no longer supported. |

## Methods

### Retrieval

`Retrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a retrieval tool that model can call to access external knowledge.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexEndpointRequest -->

# Class UpdateIndexEndpointRequest (1.134.0)

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexEndpointRequest

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeRequest -->

# Class DeleteNotebookRuntimeRequest (1.134.0)

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### DeleteNotebookRuntimeRequest

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesRequest -->

# Class ImportFeatureValuesRequest (1.134.0)

`ImportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ImportFeatureValues.

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
`avro_source` |
This field is a member of `oneof` _ `source` .
|
`bigquery_source` |
This field is a member of `oneof` _ `source` .
|
`csv_source` |
This field is a member of `oneof` _ `source` .
|
`feature_time_field` |
`str`
Source column that holds the Feature timestamp for all Feature values in each entity. This field is a member of `oneof` _ `feature_time_source` .
|
`feature_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Single Feature timestamp for all entities being imported. The timestamp must not have higher than millisecond precision. This field is a member of `oneof` _ `feature_time_source` .
|
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`
|
`entity_id_field` |
`str`
Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity_id. |
`feature_specs` |
`MutableSequence[`
Required. Specifications defining which Feature values to import from the entity. The request fails if no feature_specs are provided, and having multiple feature_specs for one Feature is not allowed. |
`disable_online_serving` |
`bool`
If set, data will not be imported for online serving. This is typically used for backfilling, where Feature generation timestamps are not in the timestamp range needed for online serving. |
`worker_count` |
`int`
Specifies the number of workers that are used to write data to the Featurestore. Consider the online serving capacity that you require to achieve the desired import throughput without interfering with online serving. The value must be positive, and less than or equal to 100. If not set, defaults to using 1 worker. The low count ensures minimal impact on online serving performance. |
`disable_ingestion_analysis` |
`bool`
If true, API doesn't start ingestion analysis pipeline. |

## Classes

### FeatureSpec

`FeatureSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines the Feature value(s) to import.

## Methods

### ImportFeatureValuesRequest

`ImportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ImportFeatureValues.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationParameters -->

# Class ExplanationParameters (1.134.0)

`ExplanationParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters to configure explaining for Model's predictions.

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
`sampled_shapley_attribution` |
An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: https://arxiv.org/abs/1306.4265. This field is a member of `oneof` _ `method` .
|
`integrated_gradients_attribution` |
An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: https://arxiv.org/abs/1703.01365 This field is a member of `oneof` _ `method` .
|
`xrai_attribution` |
An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: https://arxiv.org/abs/1906.02825 XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead. This field is a member of `oneof` _ `method` .
|
`examples` |
Example-based explanations that returns the nearest neighbors from the provided dataset. This field is a member of `oneof` _ `method` .
|
`top_k` |
`int`
If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs. |
`output_indices` |
`google.protobuf.struct_pb2.ListValue`
If populated, only returns attributions that have output_index contained in output_indices. It must be an ndarray of integers, with the same shape of the output it's explaining. If not populated, returns attributions for top_k indices of outputs. If neither top_k nor output_indices is populated, returns the argmax index of the outputs. Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes). |

## Methods

### ExplanationParameters

`ExplanationParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters to configure explaining for Model's predictions.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service -->

# Package endpoint_service (1.134.0)

API documentation for `aiplatform_v1.services.endpoint_service`

package.

## Classes

[EndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient)

A service for managing Vertex AI's Endpoints.

[EndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient)

A service for managing Vertex AI's Endpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers)

API documentation for `aiplatform_v1.services.endpoint_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse -->

# Class ListBatchPredictionJobsResponse (1.134.0)

```
ListBatchPredictionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListBatchPredictionJobs

## Attributes |
|
|---|---|
Name |
Description |
`batch_prediction_jobs` |
`MutableSequence[`
List of BatchPredictionJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListBatchPredictionJobsRequest.page_token to obtain that page. |

## Methods

### ListBatchPredictionJobsResponse

```
ListBatchPredictionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListBatchPredictionJobs

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial.State -->

# Class State (1.134.0)

`State(value)`


Describes a Trial state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The Trial state is unspecified. |
`REQUESTED` |
Indicates that a specific Trial has been requested, but it has not yet been suggested by the service. |
`ACTIVE` |
Indicates that the Trial has been suggested. |
`STOPPING` |
Indicates that the Trial should stop according to the service. |
`SUCCEEDED` |
Indicates that the Trial is completed successfully. |
`INFEASIBLE` |
Indicates that the Trial should not be attempted again. The service will set a Trial to INFEASIBLE when it's done but missing the final_measurement. |

## Methods

### State

`State(value)`


Describes a Trial state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecasting -->

# Class AutoMlForecasting (1.134.0)

`AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Forecasting Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlForecasting

`AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Forecasting Model.

### AutoMlForecasting

`AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Forecasting Model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskDetail -->

# Class PipelineTaskDetail (1.134.0)

`PipelineTaskDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of a task execution.

## Attributes |
|
|---|---|
Name |
Description |
`task_id` |
`int`
Output only. The system generated ID of the task. |
`parent_task_id` |
`int`
Output only. The id of the parent task if the task is within a component scope. Empty if the task is at the root level. |
`task_name` |
`str`
Output only. The user specified name of the task that is defined in pipeline_spec. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Task create time. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Task start time. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Task end time. |
`executor_detail` |
Output only. The detailed execution info. |
`state` |
Output only. State of the task. |
`execution` |
Output only. The execution metadata of the task. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during task execution. Only populated when the task's state is FAILED or CANCELLED. |
`pipeline_task_status` |
`MutableSequence[`
Output only. A list of task status. This field keeps a record of task status evolving over time. |
`inputs` |
`MutableMapping[str, `
Output only. The runtime input artifacts of the task. |
`outputs` |
`MutableMapping[str, `
Output only. The runtime output artifacts of the task. |
`task_unique_name` |
`str`
Output only. The unique name of a task. This field is used by rerun pipeline job. Console UI and Vertex AI SDK will support triggering pipeline job reruns. The name is constructed by concatenating all the parent tasks name with the task name. For example, if a task named "child_task" has a parent task named "parent_task_1" and parent task 1 has a parent task named "parent_task_2", the task unique name will be "parent_task_2.parent_task_1.child_task". |

## Classes

### ArtifactList

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.

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

### PipelineTaskStatus

`PipelineTaskStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single record of the task status.

### State

`State(value)`


Specifies state of TaskExecution

## Methods

### PipelineTaskDetail

`PipelineTaskDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of a task execution.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest -->

# Class ImportFeatureValuesRequest (1.134.0)

`ImportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ImportFeatureValues.

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
`avro_source` |
This field is a member of `oneof` _ `source` .
|
`bigquery_source` |
This field is a member of `oneof` _ `source` .
|
`csv_source` |
This field is a member of `oneof` _ `source` .
|
`feature_time_field` |
`str`
Source column that holds the Feature timestamp for all Feature values in each entity. This field is a member of `oneof` _ `feature_time_source` .
|
`feature_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Single Feature timestamp for all entities being imported. The timestamp must not have higher than millisecond precision. This field is a member of `oneof` _ `feature_time_source` .
|
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`
|
`entity_id_field` |
`str`
Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity_id. |
`feature_specs` |
`MutableSequence[`
Required. Specifications defining which Feature values to import from the entity. The request fails if no feature_specs are provided, and having multiple feature_specs for one Feature is not allowed. |
`disable_online_serving` |
`bool`
If set, data will not be imported for online serving. This is typically used for backfilling, where Feature generation timestamps are not in the timestamp range needed for online serving. |
`worker_count` |
`int`
Specifies the number of workers that are used to write data to the Featurestore. Consider the online serving capacity that you require to achieve the desired import throughput without interfering with online serving. The value must be positive, and less than or equal to 100. If not set, defaults to using 1 worker. The low count ensures minimal impact on online serving performance. |
`disable_ingestion_analysis` |
`bool`
If true, API doesn't start ingestion analysis pipeline. |

## Classes

### FeatureSpec

`FeatureSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines the Feature value(s) to import.

## Methods

### ImportFeatureValuesRequest

`ImportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ImportFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient -->

# Class MatchServiceAsyncClient (1.134.0)

```
MatchServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


MatchService is a Google managed service for efficient vector similarity search at scale.

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
`MatchServiceTransport` |
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

### MatchServiceAsyncClient

```
MatchServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MatchServiceTransport,Callable[..., MatchServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsResponse
```


Finds the nearest neighbors of each vector within the request.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_find_neighbors():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceAsyncClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.FindNeighbors. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
The response message for MatchService.FindNeighbors. |

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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport
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

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsResponse
```


Reads the datapoints/vectors of the given IDs. A maximum of 1000 datapoints can be retrieved in a batch.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceAsyncClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
The response message for MatchService.ReadIndexDatapoints. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsResponse.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`datapoint` |
The datapoint of the neighbor. Note that full datapoints are returned only when "return_full_datapoint" is set to true. Otherwise, only the "datapoint_id" and "crowding_tag" fields are populated. |
`distance` |
`float`
The distance between the neighbor and the dense embedding query. |
`sparse_distance` |
`float`
The distance between the neighbor and the query sparse_embedding. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.ExportFormat.ExportableContent -->

# Class ExportableContent (1.134.0)

`ExportableContent(value)`


The Model content that can be exported.

## Enums |
|
|---|---|
Name |
Description |
`EXPORTABLE_CONTENT_UNSPECIFIED` |
Should not be used. |
`ARTIFACT` |
Model artifact and any of its supported files. Will be exported to the location specified by the `artifactDestination` field of the ExportModelRequest.output_config object. |
`IMAGE` |
The container image that is to be used when deploying this Model. Will be exported to the location specified by the `imageDestination` field of the ExportModelRequest.output_config object. |

## Methods

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse -->

# Class ListTensorboardRunsResponse (1.134.0)

`ListTensorboardRunsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_runs` |
`MutableSequence[`
The TensorboardRuns mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardRunsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardRunsResponse

`ListTensorboardRunsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboardRuns.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse -->

# Class ListMetadataSchemasResponse (1.134.0)

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_schemas` |
`MutableSequence[`
The MetadataSchemas found for the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataSchemasRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataSchemasResponse

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationParameters -->

# Class ExplanationParameters (1.134.0)

`ExplanationParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters to configure explaining for Model's predictions.

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
`sampled_shapley_attribution` |
An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: https://arxiv.org/abs/1306.4265. This field is a member of `oneof` _ `method` .
|
`integrated_gradients_attribution` |
An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: https://arxiv.org/abs/1703.01365 This field is a member of `oneof` _ `method` .
|
`xrai_attribution` |
An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: https://arxiv.org/abs/1906.02825 XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead. This field is a member of `oneof` _ `method` .
|
`examples` |
Example-based explanations that returns the nearest neighbors from the provided dataset. This field is a member of `oneof` _ `method` .
|
`top_k` |
`int`
If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs. |
`output_indices` |
`google.protobuf.struct_pb2.ListValue`
If populated, only returns attributions that have output_index contained in output_indices. It must be an ndarray of integers, with the same shape of the output it's explaining. If not populated, returns attributions for top_k indices of outputs. If neither top_k nor output_indices is populated, returns the argmax index of the outputs. Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes). |

## Methods

### ExplanationParameters

`ExplanationParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters to configure explaining for Model's predictions.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.gen_ai_tuning_service.pagers`

module.

## Classes

[ListTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager)

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

[ListTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager)

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Retrieval -->

# Class Retrieval (1.134.0)

`Retrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a retrieval tool that model can call to access external knowledge.

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
`vertex_ai_search` |
Set to use data source powered by Vertex AI Search. This field is a member of `oneof` _ `source` .
|
`vertex_rag_store` |
Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService. This field is a member of `oneof` _ `source` .
|
`disable_attribution` |
`bool`
Optional. Deprecated. This option is no longer supported. |

## Methods

### Retrieval

`Retrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a retrieval tool that model can call to access external knowledge.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest -->

# Class DeleteNotebookRuntimeTemplateRequest (1.134.0)

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### DeleteNotebookRuntimeTemplateRequest

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization.Type -->

# Class Type (1.134.0)

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution].

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Should not be used. |
`PIXELS` |
Shows which pixel contributed to the image prediction. |
`OUTLINES` |
Shows which region contributed to the image prediction by outlining the region. |

## Methods

### Type

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution].

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskDetail -->

# Class PipelineTaskDetail (1.134.0)

`PipelineTaskDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of a task execution.

## Attributes |
|
|---|---|
Name |
Description |
`task_id` |
`int`
Output only. The system generated ID of the task. |
`parent_task_id` |
`int`
Output only. The id of the parent task if the task is within a component scope. Empty if the task is at the root level. |
`task_name` |
`str`
Output only. The user specified name of the task that is defined in pipeline_spec. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Task create time. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Task start time. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Task end time. |
`executor_detail` |
Output only. The detailed execution info. |
`state` |
Output only. State of the task. |
`execution` |
Output only. The execution metadata of the task. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during task execution. Only populated when the task's state is FAILED or CANCELLED. |
`pipeline_task_status` |
`MutableSequence[`
Output only. A list of task status. This field keeps a record of task status evolving over time. |
`inputs` |
`MutableMapping[str, `
Output only. The runtime input artifacts of the task. |
`outputs` |
`MutableMapping[str, `
Output only. The runtime output artifacts of the task. |
`task_unique_name` |
`str`
Output only. The unique name of a task. This field is used by pipeline job reruns. Console UI and Vertex AI SDK will support triggering pipeline job reruns. The name is constructed by concatenating all the parent tasks' names with the task name. For example, if a task named "child_task" has a parent task named "parent_task_1" and parent task 1 has a parent task named "parent_task_2", the task unique name will be "parent_task_2.parent_task_1.child_task". |

## Classes

### ArtifactList

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.

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

### PipelineTaskStatus

`PipelineTaskStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single record of the task status.

### State

`State(value)`


Specifies state of TaskExecution

## Methods

### PipelineTaskDetail

`PipelineTaskDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime detail of a task execution.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextExtractionPredictionResult -->

# Class TextExtractionPredictionResult (1.134.0)

```
TextExtractionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Extraction.

## Attributes |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[int]`
The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly. |
`display_names` |
`MutableSequence[str]`
The display names of the AnnotationSpecs that had been identified, order matches the IDs. |
`text_segment_start_offsets` |
`MutableSequence[int]`
The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet. |
`text_segment_end_offsets` |
`MutableSequence[int]`
The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet. |
`confidences` |
`MutableSequence[float]`
The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids. |

## Methods

### TextExtractionPredictionResult

```
TextExtractionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Extraction.

### TextExtractionPredictionResult

```
TextExtractionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Text Extraction.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDatasetVersionRequest -->

# Class GetDatasetVersionRequest (1.134.0)

`GetDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDatasetVersion. Next ID: 4

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetDatasetVersionRequest

`GetDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDatasetVersion. Next ID: 4

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValue.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Attribute |
|
|---|---|
Name |
Description |
`generate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Feature generation timestamp. Typically, it is provided by user at feature ingestion time. If not, feature store will use the system timestamp when the data is ingested into feature store. Legacy Feature Store: For streaming ingestion, the time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest -->

# Class UndeployModelRequest (1.134.0)

`UndeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UndeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource from which to undeploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the Endpoint. |
`traffic_split` |
`MutableMapping[str, int]`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. |

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

### UndeployModelRequest

`UndeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UndeployModel.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.DataformRepositorySource -->

# Class DataformRepositorySource (1.134.0)

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`dataform_repository_resource_name` |
`str`
The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}`
|
`commit_sha` |
`str`
The commit SHA to read repository with. If unset, the file will be read at HEAD. |

## Methods

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelDeploymentMonitoringJobRequest -->

# Class GetModelDeploymentMonitoringJobRequest (1.134.0)

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### GetModelDeploymentMonitoringJobRequest

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TimeSeriesDataPoint -->

# Class TimeSeriesDataPoint (1.134.0)

`TimeSeriesDataPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardTimeSeries data point.

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
`scalar` |
A scalar value. This field is a member of `oneof` _ `value` .
|
`tensor` |
A tensor value. This field is a member of `oneof` _ `value` .
|
`blobs` |
A blob sequence value. This field is a member of `oneof` _ `value` .
|
`wall_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Wall clock timestamp when this data point is generated by the end user. |
`step` |
`int`
Step index of this data point within the run. |

## Methods

### TimeSeriesDataPoint

`TimeSeriesDataPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardTimeSeries data point.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoActionRecognitionPredictionInstance -->

# Class VideoActionRecognitionPredictionInstance (1.134.0)

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoActionRecognitionPredictionInstance

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

### VideoActionRecognitionPredictionInstance

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service -->

# Package index_service (1.134.0)

API documentation for `aiplatform_v1.services.index_service`

package.

## Classes

[IndexServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient)

A service for creating and managing Vertex AI's Index resources.

[IndexServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient)

A service for creating and managing Vertex AI's Index resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers)

API documentation for `aiplatform_v1.services.index_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest -->

# Class DeleteNotebookRuntimeRequest (1.134.0)

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### DeleteNotebookRuntimeRequest

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse -->

# Class ListBatchPredictionJobsResponse (1.134.0)

```
ListBatchPredictionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListBatchPredictionJobs

## Attributes |
|
|---|---|
Name |
Description |
`batch_prediction_jobs` |
`MutableSequence[`
List of BatchPredictionJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListBatchPredictionJobsRequest.page_token to obtain that page. |

## Methods

### ListBatchPredictionJobsResponse

```
ListBatchPredictionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListBatchPredictionJobs

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeRequest -->

# Class UpgradeNotebookRuntimeRequest (1.134.0)

```
UpgradeNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpgradeNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### UpgradeNotebookRuntimeRequest

```
UpgradeNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpgradeNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest -->

# Class UndeployModelRequest (1.134.0)

`UndeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UndeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource from which to undeploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the Endpoint. |
`traffic_split` |
`MutableMapping[str, int]`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. |

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

### UndeployModelRequest

`UndeployModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UndeployModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimeSeriesDataPoint -->

# Class TimeSeriesDataPoint (1.134.0)

`TimeSeriesDataPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardTimeSeries data point.

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
`scalar` |
A scalar value. This field is a member of `oneof` _ `value` .
|
`tensor` |
A tensor value. This field is a member of `oneof` _ `value` .
|
`blobs` |
A blob sequence value. This field is a member of `oneof` _ `value` .
|
`wall_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Wall clock timestamp when this data point is generated by the end user. |
`step` |
`int`
Step index of this data point within the run. |

## Methods

### TimeSeriesDataPoint

`TimeSeriesDataPoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TensorboardTimeSeries data point.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.ExportFormat.ExportableContent -->

# Class ExportableContent (1.134.0)

`ExportableContent(value)`


The Model content that can be exported.

## Enums |
|
|---|---|
Name |
Description |
`EXPORTABLE_CONTENT_UNSPECIFIED` |
Should not be used. |
`ARTIFACT` |
Model artifact and any of its supported files. Will be exported to the location specified by the `artifactDestination` field of the ExportModelRequest.output_config object. |
`IMAGE` |
The container image that is to be used when deploying this Model. Will be exported to the location specified by the `imageDestination` field of the ExportModelRequest.output_config object. |

## Methods

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SecretRef -->

# Class SecretRef (1.134.0)

`SecretRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret_name}. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias. |

## Methods

### SecretRef

`SecretRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse -->

# Class ListMetadataSchemasResponse (1.134.0)

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_schemas` |
`MutableSequence[`
The MetadataSchemas found for the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataSchemasRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataSchemasResponse

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service -->

# Package metadata_service (1.134.0)

API documentation for `aiplatform_v1.services.metadata_service`

package.

## Classes

[MetadataServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient)

Service for reading and writing metadata entries.

[MetadataServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient)

Service for reading and writing metadata entries.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers)

API documentation for `aiplatform_v1.services.metadata_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDataKey -->

# Class FeatureViewDataKey (1.134.0)

`FeatureViewDataKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Lookup key for a feature view.

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
`key` |
`str`
String key to use for lookup. This field is a member of `oneof` _ `key_oneof` .
|
`composite_key` |
The actual Entity ID will be composed from this struct. This should match with the way ID is defined in the FeatureView spec. This field is a member of `oneof` _ `key_oneof` .
|

## Classes

### CompositeKey

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

## Methods

### FeatureViewDataKey

`FeatureViewDataKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Lookup key for a feature view.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob.LatestMonitoringPipelineMetadata -->

# Class LatestMonitoringPipelineMetadata (1.134.0)

```
LatestMonitoringPipelineMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


All metadata of most recent monitoring pipelines.

## Attributes |
|
|---|---|
Name |
Description |
`run_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time that most recent monitoring pipelines that is related to this run. |
`status` |
`google.rpc.status_pb2.Status`
The status of the most recent monitoring pipeline. |

## Methods

### LatestMonitoringPipelineMetadata

```
LatestMonitoringPipelineMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


All metadata of most recent monitoring pipelines.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.DataformRepositorySource -->

# Class DataformRepositorySource (1.134.0)

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`dataform_repository_resource_name` |
`str`
The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}`
|
`commit_sha` |
`str`
The commit SHA to read repository with. If unset, the file will be read at HEAD. |

## Methods

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelDeploymentMonitoringJobRequest -->

# Class GetModelDeploymentMonitoringJobRequest (1.134.0)

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### GetModelDeploymentMonitoringJobRequest

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReplicatedVoiceConfig -->

# Class ReplicatedVoiceConfig (1.134.0)

`ReplicatedVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for the replicated voice to use.

## Attributes |
|
|---|---|
Name |
Description |
`mime_type` |
`str`
Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents
16-bit signed little-endian wav data, with a 24kHz sampling
rate. `mime_type` will default to `audio/wav` if not
set.
|
`voice_sample_audio` |
`bytes`
Optional. The sample of the custom voice. |

## Methods

### ReplicatedVoiceConfig

`ReplicatedVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for the replicated voice to use.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.DirectContentsSource -->

# Class DirectContentsSource (1.134.0)

`DirectContentsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a direct source of content from which to generate the memories.

## Attribute |
|
|---|---|
Name |
Description |
`events` |
`MutableSequence[`
Required. The source content (i.e. chat history) to generate memories from. |

## Classes

### Event

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single piece of conversation from which to generate memories.

## Methods

### DirectContentsSource

`DirectContentsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a direct source of content from which to generate the memories.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoHyperParameters -->

# Class VeoHyperParameters (1.134.0)

`VeoHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Veo.

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. |
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. |
`tuning_task` |
Optional. The tuning task. Either I2V or T2V. |

## Classes

### TuningTask

`TuningTask(value)`


An enum defining the tuning task used for Veo.

## Methods

### VeoHyperParameters

`VeoHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Veo.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsRequest -->

# Class ListEndpointsRequest (1.134.0)

`ListEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.ListEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the Endpoints. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `endpoint` supports `=` and `!=` . `endpoint`
represents the Endpoint ID, i.e. the last segment of the
Endpoint's [resource
name][google.cloud.aiplatform.v1beta1.Endpoint.name].
- `display_name` supports `=` and `!=` .
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- `labels.key:*` or `labels:key` - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `base_model_name` only supports `=` .
Some examples:
- `endpoint=1`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `baseModelName="text-bison"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListEndpointsResponse.next_page_token of the previous EndpointService.ListEndpoints call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |

## Methods

### ListEndpointsRequest

`ListEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.ListEndpoints.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse -->

# Class ListModelVersionsResponse (1.134.0)

`ListModelVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModelVersions

## Attributes |
|
|---|---|
Name |
Description |
`models` |
`MutableSequence[`
List of Model versions in the requested page. In the returned Model name field, version ID instead of regvision tag will be included. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListModelVersionsRequest.page_token to obtain that page. |

## Methods

### ListModelVersionsResponse

`ListModelVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModelVersions

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service -->

# Package tensorboard_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.tensorboard_service`

package.

## Classes

[TensorboardServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient)

TensorboardService

[TensorboardServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceClient)

TensorboardService

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers)

API documentation for `aiplatform_v1beta1.services.tensorboard_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiExample -->

# Class GeminiExample (1.134.0)

`GeminiExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Format for Gemini examples used for Vertex Multimodal datasets.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Optional. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`
Tuned model endpoint format:
`projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. |
`system_instruction` |
Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph. This field is a member of `oneof` _ `_system_instruction` .
|
`cached_content` |
`str`
Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`
|
`tools` |
`MutableSequence[`
Optional. A list of `Tools` the model may use to generate
the next response.
A `Tool` is a piece of code that enables the system to
interact with external systems to perform an action, or set
of actions, outside of knowledge and scope of the model.
|
`tool_config` |
Optional. Tool config. This config is shared for all tools provided in the request. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only. Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter. |
`safety_settings` |
`MutableSequence[`
Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates. |
`generation_config` |
Optional. Generation config. |

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

### GeminiExample

`GeminiExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Format for Gemini examples used for Vertex Multimodal datasets.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse -->

# Class ListFeatureMonitorsResponse (1.134.0)

`ListFeatureMonitorsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureMonitors.

## Attributes |
|
|---|---|
Name |
Description |
`feature_monitors` |
`MutableSequence[`
The FeatureMonitors matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureMonitorsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureMonitorsResponse

`ListFeatureMonitorsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureMonitors.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValue.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Attribute |
|
|---|---|
Name |
Description |
`generate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Feature generation timestamp. Typically, it is provided by user at feature ingestion time. If not, feature store will use the system timestamp when the data is ingested into feature store. Legacy Feature Store: For streaming ingestion, the time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoActionRecognitionPredictionInstance -->

# Class VideoActionRecognitionPredictionInstance (1.134.0)

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoActionRecognitionPredictionInstance

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

### VideoActionRecognitionPredictionInstance

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.
