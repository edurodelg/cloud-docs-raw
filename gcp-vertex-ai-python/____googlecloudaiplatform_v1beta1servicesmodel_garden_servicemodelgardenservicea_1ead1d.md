---
merged_at: 2026-01-28T15:11:44.784452
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient -->

# Class ModelGardenServiceAsyncClient (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient -->

# Class SessionServiceAsyncClient (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient -->

# Class MemoryBankServiceAsyncClient (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesPager -->

# Class ListIndexesPager (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQuerySource -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation -->

# Class Transformation (1.135.0)

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

# Class Schedule (1.135.0)

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

# Class Documentation (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceResult -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardExperiment -->

# Class TensorboardExperiment (1.135.0)

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

# Class ReviewSnippet (1.135.0)

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

# Class UpdateMemoryOperationMetadata (1.135.0)

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

# Class DeleteMemoryOperationMetadata (1.135.0)

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

# Package llm_utility_service (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometInstance -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTuningJobRequest -->

# Class GetTuningJobRequest (1.135.0)

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

# Class GoogleSearchRetrieval (1.135.0)

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

# Class PairwiseQuestionAnsweringQualityResult (1.135.0)

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

# Class Parent (1.135.0)

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

# Class CreateMemoryOperationMetadata (1.135.0)

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

# Class PageSpan (1.135.0)

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

# Class ImportIndexOperationMetadata (1.135.0)

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

# Class Transformation (1.135.0)

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

# Class ListStudiesPager (1.135.0)

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

# Class ModelMonitoringConfig (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UrlMetadata -->

# Class UrlMetadata (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient -->

# Class DeploymentResourcePoolServiceAsyncClient (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchInstance -->

# Class TrajectoryExactMatchInstance (1.135.0)

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

# Package model_garden_service (1.135.0)

API documentation for `aiplatform_v1.services.model_garden_service`

package.

## Classes

[ModelGardenServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_garden_service.ModelGardenServiceAsyncClient)

The interface of Model Garden Service.

[ModelGardenServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_garden_service.ModelGardenServiceClient)

The interface of Model Garden Service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagCorpusRequest -->

# Class GetRagCorpusRequest (1.135.0)

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

# Class TensorboardExperiment (1.135.0)

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

# Class DeleteDatasetRequest (1.135.0)

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

# Class ModelRoutingPreference (1.135.0)

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

# Class PairwiseQuestionAnsweringQualityResult (1.135.0)

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

# Class UpdateFeaturestoreRequest (1.135.0)

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

# Package evaluation_service (1.135.0)

API documentation for `aiplatform_v1beta1.services.evaluation_service`

package.

## Classes

[EvaluationServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient)

Vertex AI Online Evaluation Service.

[EvaluationServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient)

Vertex AI Online Evaluation Service.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityInput -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookSoftwareConfig -->

# Class NotebookSoftwareConfig (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail.ProcessedDataset -->

# Class ProcessedDataset (1.135.0)

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

# Class Documentation (1.135.0)

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

# Class TrafficType (1.135.0)

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

# Class Claim (1.135.0)

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

# Class ReviewSnippet (1.135.0)

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

# Class GetDatasetRequest (1.135.0)

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

# Class PlaceAnswerSources (1.135.0)

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

# Class GoogleSearchRetrieval (1.135.0)

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

# Class ListModelsPager (1.135.0)

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

# Class SearchExamplesRequest (1.135.0)

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

# Class UpdateFeaturestoreRequest (1.135.0)

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

# Class GetTuningJobRequest (1.135.0)

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

# Class CancelCustomJobRequest (1.135.0)

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

# Class PageSpan (1.135.0)

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

# Class GetRagFileRequest (1.135.0)

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

# Class NotebookSoftwareConfig (1.135.0)

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

# Class MetricxInstance (1.135.0)

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

# Class UrlMetadata (1.135.0)

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

# Class MutateDeployedIndexResponse (1.135.0)

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

# Class Claim (1.135.0)

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

# Class AutoRoutingMode (1.135.0)

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

# Class NotebookRuntimeType (1.135.0)

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

# Class GetRagCorpusRequest (1.135.0)

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

# Class Context (1.135.0)

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

# Class ListDatasetsPager (1.135.0)

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

# Class ListTrialsPager (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient -->

# Class IndexServiceClient (1.135.0)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model -->

# Class Model (1.135.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The resource name of the Model. |
`version_id` |
`str`
Output only. Immutable. The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation. |
`version_aliases` |
`MutableSequence[str]`
User provided version aliases so that a model version can be referenced via alias (i.e. `projects/{project}/locations/{location}/models/{model_id}@{version_alias}`
instead of auto-generated version id (i.e.
`projects/{project}/locations/{location}/models/{model_id}@{version_id})` .
The format is `a-z][a-zA-Z0-9-]` {0,126}[a-z0-9] to
distinguish from version_id. A default version alias will be
created for the first version of the model, and there must
be exactly one default version alias for a model.
|
`version_create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was created. |
`version_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was most recently updated. |
`display_name` |
`str`
Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Model. |
`version_description` |
`str`
The description of this version. |
`default_checkpoint_id` |
`str`
The default checkpoint id of a model version. |
`predict_schemata` |
The schemata that describe formats of the Model's predictions and explanations as given and returned via PredictionService.Predict and PredictionService.Explain. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
Immutable. An additional information about the Model; the schema of the metadata can be found in metadata_schema. Unset if the Model does not have any additional information. |
`supported_export_formats` |
`MutableSequence[`
Output only. The formats in which this Model may be exported. If empty, this Model is not available for export. |
`training_pipeline` |
`str`
Output only. The resource name of the TrainingPipeline that uploaded this Model, if any. |
`pipeline_job` |
`str`
Optional. This field is populated if the model is produced by a pipeline job. |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. The specification is ingested upon ModelService.UploadModel, and all binaries it contains are copied and stored internally by Vertex AI. Not required for AutoML Models. |
`artifact_uri` |
`str`
Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models. |
`supported_deployment_resources_types` |
`MutableSequence[`
Output only. When this Model is deployed, its prediction resources are described by the `prediction_resources`
field of the
Endpoint.deployed_models
object. Because not all Models support all resource
configuration types, the configuration types this Model
supports are listed here. If no configuration types are
listed, the Model cannot be deployed to an
Endpoint and does not
support online predictions
(PredictionService.Predict
or
PredictionService.Explain).
Such a Model can serve predictions by using a
BatchPredictionJob,
if it has at least one entry each in
supported_input_storage_formats
and
supported_output_storage_formats.
|
`supported_input_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.input_config. If PredictSchemata.instance_schema_uri exists, the instances should be given as per that schema. The possible formats are: - `jsonl` The JSON Lines format, where each instance is a
single line. Uses
GcsSource.
- `csv` The CSV format, where each instance is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsSource.
- `tf-record` The TFRecord format, where each instance is
a single record in tfrecord syntax. Uses
GcsSource.
- `tf-record-gzip` Similar to `tf-record` , but the file
is gzipped. Uses
GcsSource.
- `bigquery` Each instance is a single row in BigQuery.
Uses
BigQuerySource.
- `file-list` Each line of the file is the location of an
instance to process, uses `gcs_source` field of the
InputConfig
object.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`supported_output_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.output_config. If both PredictSchemata.instance_schema_uri and PredictSchemata.prediction_schema_uri exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema). The possible formats are: - `jsonl` The JSON Lines format, where each prediction is
a single line. Uses
GcsDestination.
- `csv` The CSV format, where each prediction is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsDestination.
- `bigquery` Each prediction is a single row in a BigQuery
table, uses
BigQueryDestination
.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was uploaded into Vertex AI. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was most recently updated. |
`deployed_models` |
`MutableSequence[`
Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to Endpoints in different Locations. |
`explanation_spec` |
The default explanation specification for this Model. The Model can be used for [requesting explanation][google.cloud.aiplatform.v1.PredictionService.Explain] after being deployed if it is populated. The Model can be used for [batch explanation][google.cloud.aiplatform.v1.BatchPredictionJob.generate_explanation] if it is populated. All fields of the explanation_spec can be overridden by explanation_spec of DeployModelRequest.deployed_model, or explanation_spec of BatchPredictionJob. If the default explanation specification is not set for this Model, this Model can still be used for [requesting explanation][google.cloud.aiplatform.v1.PredictionService.Explain] by setting explanation_spec of DeployModelRequest.deployed_model and for [batch explanation][google.cloud.aiplatform.v1.BatchPredictionJob.generate_explanation] by setting explanation_spec of BatchPredictionJob. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`data_stats` |
Stats of data used for training or evaluating the Model. Only populated when the Model is trained by a TrainingPipeline with data_input_config. |
`encryption_spec` |
Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key. |
`model_source_info` |
Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden. |
`original_model_info` |
Output only. If this Model is a copy of another Model, this contains info about the original. |
`metadata_artifact` |
`str`
Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .
|
`base_model_source` |
Optional. User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`checkpoints` |
`MutableSequence[`
Optional. Output only. The checkpoints of the model. |

## Classes

### BaseModelSource

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DataStats

`DataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of data used for train or evaluate the Model.

### DeploymentResourcesType

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

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

### OriginalModelInfo

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

## Methods

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsPager -->

# Class ListNasJobsPager (1.135.0)

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

## Methods

### ListNasJobsPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.AutoRoutingMode.ModelRoutingPreference -->

# Class ModelRoutingPreference (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest -->

# Class DeleteDatasetRequest (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.RagManagedDb.ANN -->

# Class ANN (1.135.0)

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

## Attributes |
|
|---|---|
Name |
Description |
`tree_depth` |
`int`
The depth of the tree-based structure. Only depth values of 2 and 3 are supported. Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that. Default value is 2. |
`leaf_count` |
`int`
Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid. Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus). Default value is 500. |

## Methods

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringHelpfulnessResult -->

# Class QuestionAnsweringHelpfulnessResult (1.135.0)

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering helpfulness score. |
`confidence` |
`float`
Output only. Confidence for question answering helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringHelpfulnessResult

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessResult -->

# Class QuestionAnsweringCorrectnessResult (1.135.0)

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Correctness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering correctness score. |
`confidence` |
`float`
Output only. Confidence for question answering correctness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringCorrectnessResult

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSchema.FieldSchema -->

# Class FieldSchema (1.135.0)

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Field name. |
`data_type` |
`str`
Supported data types are: `float` `integer` `boolean`
`string` `categorical`
|
`repeated` |
`bool`
Describes if the schema field is an array of given data type. |

## Methods

### FieldSchema

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor.ModelMonitoringTarget.VertexModelSource -->

# Class VertexModelSource (1.135.0)

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Model resource name. Format: projects/{project}/locations/{location}/models/{model}. |
`model_version_id` |
`str`
Model version id. |

## Methods

### VertexModelSource

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.DecayCurveAutomatedStoppingSpec -->

# Class DecayCurveAutomatedStoppingSpec (1.135.0)

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if Measurement.elapsed_duration is used as the x-axis of each Trials Decay Curve. Otherwise, Measurement.step_count will be used as the x-axis. |

## Methods

### DecayCurveAutomatedStoppingSpec

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob -->

# Class CustomJob (1.135.0)

```
CustomJob(
display_name: str,
worker_pool_specs: typing.Union[
typing.List[typing.Dict],
typing.List[google.cloud.aiplatform_v1.types.custom_job.WorkerPoolSpec],
],
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
)
```


Vertex AI Custom Job.

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
CustomJob should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the CustomJob is not peered with any network.

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

### CustomJob

```
CustomJob(
display_name: str,
worker_pool_specs: typing.Union[
typing.List[typing.Dict],
typing.List[google.cloud.aiplatform_v1.types.custom_job.WorkerPoolSpec],
],
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
)
```


Constructs a Custom Job with Worker Pool Specs.

```
Example usage:
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
my_job = aiplatform.CustomJob(
display_name='my_job',
worker_pool_specs=worker_pool_specs,
labels={'my_key': 'my_value'},
)
my_job.run()
```


For more information on configuring worker pool specs please visit:
[https://cloud.google.com/ai-platform-unified/docs/training/create-custom-job](https://cloud.google.com/ai-platform-unified/docs/training/create-custom-job)

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of the HyperparameterTuningJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`worker_pool_specs` |
`Union[List[Dict], List[aiplatform.gapic.WorkerPoolSpec]]`
Required. The spec of the worker pools including machine type and Docker image. Can provided as a list of dictionaries or list of WorkerPoolSpec proto messages. |
`base_output_dir` |
`str`
Optional. GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. |
`project` |
`str`
Optional.Project to run the custom job in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional.Location to run the custom job in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional.Custom credentials to use to run call custom job service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional.Customer-managed encryption key name for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`staging_bucket` |
`str`
Optional. Bucket for produced custom job artifacts. Overrides staging_bucket set in aiplatform.init. |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If staging bucket was not set using aiplatform.init and a staging bucket was not passed in. |

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

### from_local_script

```
from_local_script(
display_name: str,
script_path: str,
container_uri: str,
enable_autolog: bool = False,
args: typing.Optional[typing.Sequence[str]] = None,
requirements: typing.Optional[typing.Sequence[str]] = None,
environment_variables: typing.Optional[typing.Dict[str, str]] = None,
replica_count: int = 1,
machine_type: str = "n1-standard-4",
accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
accelerator_count: int = 0,
boot_disk_type: str = "pd-ssd",
boot_disk_size_gb: int = 100,
reduction_server_replica_count: int = 0,
reduction_server_machine_type: typing.Optional[str] = None,
reduction_server_container_uri: typing.Optional[str] = None,
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.CustomJob
```


Configures a custom job from a local script.

Example usage:

```
job = aiplatform.CustomJob.from_local_script(
display_name="my-custom-job",
script_path="training_script.py",
container_uri="gcr.io/cloud-aiplatform/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
replica_count=1,
args=['--dataset', 'gs://my-bucket/my-dataset',
'--model_output_uri', 'gs://my-bucket/model']
labels={'my_key': 'my_value'},
)
job.run()
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this CustomJob. |
`script_path` |
`str`
Required. Local path to training script. |
`container_uri` |
`str`
Required. Uri of the training container image to use for custom job. Support images in Artifact Registry, Container Registry, or Docker Hub. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of |
`enable_autolog` |
`bool`
Optional. If True, the Vertex Experiments autologging feature will be enabled in the CustomJob. Note that this will wrap your training script with some autologging-related code. |
`args` |
`Optional[Sequence[str]]`
Optional. Command line arguments to be passed to the Python task. |
`requirements` |
`Sequence[str]`
Optional. List of python packages dependencies of script. |
`environment_variables` |
`Dict[str, str]`
Optional. Environment variables to be passed to the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. At most 10 environment variables can be specified. The Name of the environment variable must be unique. environment_variables = { 'MY_KEY': 'MY_VALUE' } |
`replica_count` |
`int`
Optional. The number of worker replicas. If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. |
`machine_type` |
`str`
Optional. The type of machine to use for training. |
`accelerator_type` |
`str`
Optional. Hardware accelerator type. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
Optional. The number of accelerators to attach to a worker replica. |
`boot_disk_type` |
`str`
Optional. Type of the boot disk, default is |
`boot_disk_size_gb` |
`int`
Optional. Size in GB of the boot disk, default is 100GB. boot disk size must be within the range of [100, 64000]. |
`reduction_server_replica_count` |
`int`
The number of reduction server replicas, default is 0. |
`reduction_server_machine_type` |
`str`
Optional. The type of machine to use for reduction server. |
`reduction_server_container_uri` |
`str`
Optional. The Uri of the reduction server container image. See details: |
`base_output_dir` |
`str`
Optional. GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. |
`project` |
`str`
Optional. Project to run the custom job in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run the custom job in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call custom job service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key name for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`staging_bucket` |
`str`
Optional. Bucket for produced custom job artifacts. Overrides staging_bucket set in aiplatform.init. |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`tpu_topology` |
`str`
Optional. Specifies the tpu topology to be used for TPU training job. This field is required for TPU v5 versions. For details on the TPU topology, refer to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If staging bucket was not set using aiplatform.init and a staging bucket was not passed in. |

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
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
experiment_run: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun, str
]
] = None,
tensorboard: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None,
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
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`experiment` |
`Union[aiplatform.Experiment, str]`
Optional. The instance or name of an Experiment resource to which this CustomJob will upload training parameters and metrics. |
`experiment_run` |
`Union[aiplatform.ExperimentRun, str]`
Optional. The instance or name of an ExperimentRun resource to which this CustomJob will upload training parameters and metrics. This arg can only be set when |
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
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |

### submit

```
submit(
*,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
experiment_run: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun, str
]
] = None,
tensorboard: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None
) -> None
```


Submit the configured CustomJob.

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
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. |
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`experiment` |
`Union[aiplatform.Experiment, str]`
Optional. The instance or name of an Experiment resource to which this CustomJob will upload training parameters and metrics. |
`experiment_run` |
`Union[aiplatform.ExperimentRun, str]`
Optional. The instance or name of an ExperimentRun resource to which this CustomJob will upload training parameters and metrics. This arg can only be set when |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both `experiment` and `tensorboard` are specified or if `enable_autolog` is True in `CustomJob.from_local_script` but `experiment` is not specified or the specified experiment doesn't have a backing tensorboard. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model -->

# Class Model (1.134.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The resource name of the Model. |
`version_id` |
`str`
Output only. Immutable. The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation. |
`version_aliases` |
`MutableSequence[str]`
User provided version aliases so that a model version can be referenced via alias (i.e. `projects/{project}/locations/{location}/models/{model_id}@{version_alias}`
instead of auto-generated version id (i.e.
`projects/{project}/locations/{location}/models/{model_id}@{version_id})` .
The format is `a-z][a-zA-Z0-9-]` {0,126}[a-z0-9] to
distinguish from version_id. A default version alias will be
created for the first version of the model, and there must
be exactly one default version alias for a model.
|
`version_create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was created. |
`version_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was most recently updated. |
`display_name` |
`str`
Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Model. |
`version_description` |
`str`
The description of this version. |
`default_checkpoint_id` |
`str`
The default checkpoint id of a model version. |
`predict_schemata` |
The schemata that describe formats of the Model's predictions and explanations as given and returned via PredictionService.Predict and PredictionService.Explain. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
Immutable. An additional information about the Model; the schema of the metadata can be found in metadata_schema. Unset if the Model does not have any additional information. |
`supported_export_formats` |
`MutableSequence[`
Output only. The formats in which this Model may be exported. If empty, this Model is not available for export. |
`training_pipeline` |
`str`
Output only. The resource name of the TrainingPipeline that uploaded this Model, if any. |
`pipeline_job` |
`str`
Optional. This field is populated if the model is produced by a pipeline job. |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. The specification is ingested upon ModelService.UploadModel, and all binaries it contains are copied and stored internally by Vertex AI. Not required for AutoML Models. |
`artifact_uri` |
`str`
Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models. |
`supported_deployment_resources_types` |
`MutableSequence[`
Output only. When this Model is deployed, its prediction resources are described by the `prediction_resources`
field of the
Endpoint.deployed_models
object. Because not all Models support all resource
configuration types, the configuration types this Model
supports are listed here. If no configuration types are
listed, the Model cannot be deployed to an
Endpoint and does not
support online predictions
(PredictionService.Predict
or
PredictionService.Explain).
Such a Model can serve predictions by using a
BatchPredictionJob,
if it has at least one entry each in
supported_input_storage_formats
and
supported_output_storage_formats.
|
`supported_input_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.input_config. If PredictSchemata.instance_schema_uri exists, the instances should be given as per that schema. The possible formats are: - `jsonl` The JSON Lines format, where each instance is a
single line. Uses
GcsSource.
- `csv` The CSV format, where each instance is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsSource.
- `tf-record` The TFRecord format, where each instance is
a single record in tfrecord syntax. Uses
GcsSource.
- `tf-record-gzip` Similar to `tf-record` , but the file
is gzipped. Uses
GcsSource.
- `bigquery` Each instance is a single row in BigQuery.
Uses
BigQuerySource.
- `file-list` Each line of the file is the location of an
instance to process, uses `gcs_source` field of the
InputConfig
object.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`supported_output_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.output_config. If both PredictSchemata.instance_schema_uri and PredictSchemata.prediction_schema_uri exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema). The possible formats are: - `jsonl` The JSON Lines format, where each prediction is
a single line. Uses
GcsDestination.
- `csv` The CSV format, where each prediction is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsDestination.
- `bigquery` Each prediction is a single row in a BigQuery
table, uses
BigQueryDestination
.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was uploaded into Vertex AI. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was most recently updated. |
`deployed_models` |
`MutableSequence[`
Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to Endpoints in different Locations. |
`explanation_spec` |
The default explanation specification for this Model. The Model can be used for [requesting explanation][google.cloud.aiplatform.v1.PredictionService.Explain] after being deployed if it is populated. The Model can be used for [batch explanation][google.cloud.aiplatform.v1.BatchPredictionJob.generate_explanation] if it is populated. All fields of the explanation_spec can be overridden by explanation_spec of DeployModelRequest.deployed_model, or explanation_spec of BatchPredictionJob. If the default explanation specification is not set for this Model, this Model can still be used for [requesting explanation][google.cloud.aiplatform.v1.PredictionService.Explain] by setting explanation_spec of DeployModelRequest.deployed_model and for [batch explanation][google.cloud.aiplatform.v1.BatchPredictionJob.generate_explanation] by setting explanation_spec of BatchPredictionJob. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`data_stats` |
Stats of data used for training or evaluating the Model. Only populated when the Model is trained by a TrainingPipeline with data_input_config. |
`encryption_spec` |
Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key. |
`model_source_info` |
Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden. |
`original_model_info` |
Output only. If this Model is a copy of another Model, this contains info about the original. |
`metadata_artifact` |
`str`
Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .
|
`base_model_source` |
Optional. User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`checkpoints` |
`MutableSequence[`
Optional. Output only. The checkpoints of the model. |

## Classes

### BaseModelSource

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DataStats

`DataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats of data used for train or evaluate the Model.

### DeploymentResourcesType

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

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

### OriginalModelInfo

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

## Methods

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsPager -->

# Class ListNasJobsPager (1.134.0)

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

## Methods

### ListNasJobsPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.AutoRoutingMode.ModelRoutingPreference -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.RagManagedDb.ANN -->

# Class ANN (1.134.0)

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

## Attributes |
|
|---|---|
Name |
Description |
`tree_depth` |
`int`
The depth of the tree-based structure. Only depth values of 2 and 3 are supported. Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that. Default value is 2. |
`leaf_count` |
`int`
Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid. Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus). Default value is 500. |

## Methods

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringHelpfulnessResult -->

# Class QuestionAnsweringHelpfulnessResult (1.134.0)

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering helpfulness score. |
`confidence` |
`float`
Output only. Confidence for question answering helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringHelpfulnessResult

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessResult -->

# Class QuestionAnsweringCorrectnessResult (1.134.0)

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Correctness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering correctness score. |
`confidence` |
`float`
Output only. Confidence for question answering correctness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringCorrectnessResult

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSchema.FieldSchema -->

# Class FieldSchema (1.134.0)

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Field name. |
`data_type` |
`str`
Supported data types are: `float` `integer` `boolean`
`string` `categorical`
|
`repeated` |
`bool`
Describes if the schema field is an array of given data type. |

## Methods

### FieldSchema

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor.ModelMonitoringTarget.VertexModelSource -->

# Class VertexModelSource (1.134.0)

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Model resource name. Format: projects/{project}/locations/{location}/models/{model}. |
`model_version_id` |
`str`
Model version id. |

## Methods

### VertexModelSource

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.DecayCurveAutomatedStoppingSpec -->

# Class DecayCurveAutomatedStoppingSpec (1.134.0)

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if Measurement.elapsed_duration is used as the x-axis of each Trials Decay Curve. Otherwise, Measurement.step_count will be used as the x-axis. |

## Methods

### DecayCurveAutomatedStoppingSpec

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob -->

# Class CustomJob (1.134.0)

```
CustomJob(
display_name: str,
worker_pool_specs: typing.Union[
typing.List[typing.Dict],
typing.List[google.cloud.aiplatform_v1.types.custom_job.WorkerPoolSpec],
],
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
)
```


Vertex AI Custom Job.

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
CustomJob should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the CustomJob is not peered with any network.

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

### CustomJob

```
CustomJob(
display_name: str,
worker_pool_specs: typing.Union[
typing.List[typing.Dict],
typing.List[google.cloud.aiplatform_v1.types.custom_job.WorkerPoolSpec],
],
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
)
```


Constructs a Custom Job with Worker Pool Specs.

```
Example usage:
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
my_job = aiplatform.CustomJob(
display_name='my_job',
worker_pool_specs=worker_pool_specs,
labels={'my_key': 'my_value'},
)
my_job.run()
```


For more information on configuring worker pool specs please visit:
[https://cloud.google.com/ai-platform-unified/docs/training/create-custom-job](https://cloud.google.com/ai-platform-unified/docs/training/create-custom-job)

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of the HyperparameterTuningJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`worker_pool_specs` |
`Union[List[Dict], List[aiplatform.gapic.WorkerPoolSpec]]`
Required. The spec of the worker pools including machine type and Docker image. Can provided as a list of dictionaries or list of WorkerPoolSpec proto messages. |
`base_output_dir` |
`str`
Optional. GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. |
`project` |
`str`
Optional.Project to run the custom job in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional.Location to run the custom job in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional.Custom credentials to use to run call custom job service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional.Customer-managed encryption key name for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`staging_bucket` |
`str`
Optional. Bucket for produced custom job artifacts. Overrides staging_bucket set in aiplatform.init. |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If staging bucket was not set using aiplatform.init and a staging bucket was not passed in. |

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

### from_local_script

```
from_local_script(
display_name: str,
script_path: str,
container_uri: str,
enable_autolog: bool = False,
args: typing.Optional[typing.Sequence[str]] = None,
requirements: typing.Optional[typing.Sequence[str]] = None,
environment_variables: typing.Optional[typing.Dict[str, str]] = None,
replica_count: int = 1,
machine_type: str = "n1-standard-4",
accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
accelerator_count: int = 0,
boot_disk_type: str = "pd-ssd",
boot_disk_size_gb: int = 100,
reduction_server_replica_count: int = 0,
reduction_server_machine_type: typing.Optional[str] = None,
reduction_server_container_uri: typing.Optional[str] = None,
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.CustomJob
```


Configures a custom job from a local script.

Example usage:

```
job = aiplatform.CustomJob.from_local_script(
display_name="my-custom-job",
script_path="training_script.py",
container_uri="gcr.io/cloud-aiplatform/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
replica_count=1,
args=['--dataset', 'gs://my-bucket/my-dataset',
'--model_output_uri', 'gs://my-bucket/model']
labels={'my_key': 'my_value'},
)
job.run()
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this CustomJob. |
`script_path` |
`str`
Required. Local path to training script. |
`container_uri` |
`str`
Required. Uri of the training container image to use for custom job. Support images in Artifact Registry, Container Registry, or Docker Hub. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of |
`enable_autolog` |
`bool`
Optional. If True, the Vertex Experiments autologging feature will be enabled in the CustomJob. Note that this will wrap your training script with some autologging-related code. |
`args` |
`Optional[Sequence[str]]`
Optional. Command line arguments to be passed to the Python task. |
`requirements` |
`Sequence[str]`
Optional. List of python packages dependencies of script. |
`environment_variables` |
`Dict[str, str]`
Optional. Environment variables to be passed to the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. At most 10 environment variables can be specified. The Name of the environment variable must be unique. environment_variables = { 'MY_KEY': 'MY_VALUE' } |
`replica_count` |
`int`
Optional. The number of worker replicas. If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. |
`machine_type` |
`str`
Optional. The type of machine to use for training. |
`accelerator_type` |
`str`
Optional. Hardware accelerator type. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
Optional. The number of accelerators to attach to a worker replica. |
`boot_disk_type` |
`str`
Optional. Type of the boot disk, default is |
`boot_disk_size_gb` |
`int`
Optional. Size in GB of the boot disk, default is 100GB. boot disk size must be within the range of [100, 64000]. |
`reduction_server_replica_count` |
`int`
The number of reduction server replicas, default is 0. |
`reduction_server_machine_type` |
`str`
Optional. The type of machine to use for reduction server. |
`reduction_server_container_uri` |
`str`
Optional. The Uri of the reduction server container image. See details: |
`base_output_dir` |
`str`
Optional. GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. |
`project` |
`str`
Optional. Project to run the custom job in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run the custom job in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call custom job service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key name for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`staging_bucket` |
`str`
Optional. Bucket for produced custom job artifacts. Overrides staging_bucket set in aiplatform.init. |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`tpu_topology` |
`str`
Optional. Specifies the tpu topology to be used for TPU training job. This field is required for TPU v5 versions. For details on the TPU topology, refer to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If staging bucket was not set using aiplatform.init and a staging bucket was not passed in. |

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
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
experiment_run: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun, str
]
] = None,
tensorboard: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None,
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
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`experiment` |
`Union[aiplatform.Experiment, str]`
Optional. The instance or name of an Experiment resource to which this CustomJob will upload training parameters and metrics. |
`experiment_run` |
`Union[aiplatform.ExperimentRun, str]`
Optional. The instance or name of an ExperimentRun resource to which this CustomJob will upload training parameters and metrics. This arg can only be set when |
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
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |

### submit

```
submit(
*,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
experiment_run: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun, str
]
] = None,
tensorboard: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None
) -> None
```


Submit the configured CustomJob.

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
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. |
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`experiment` |
`Union[aiplatform.Experiment, str]`
Optional. The instance or name of an Experiment resource to which this CustomJob will upload training parameters and metrics. |
`experiment_run` |
`Union[aiplatform.ExperimentRun, str]`
Optional. The instance or name of an ExperimentRun resource to which this CustomJob will upload training parameters and metrics. This arg can only be set when |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both `experiment` and `tensorboard` are specified or if `enable_autolog` is True in `CustomJob.from_local_script` but `experiment` is not specified or the specified experiment doesn't have a backing tensorboard. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Context -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReservationAffinity -->

# Class ReservationAffinity (1.134.0)

`ReservationAffinity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ReservationAffinity can be used to configure a Vertex AI resource (e.g., a DeployedModel) to draw its Compute Engine resources from a Shared Reservation, or exclusively from on-demand capacity.

## Attributes |
|
|---|---|
Name |
Description |
`reservation_affinity_type` |
Required. Specifies the reservation affinity type. |
`key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and
specify the name of your reservation as its value.
|
`values` |
`MutableSequence[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. |

## Classes

### Type

`Type(value)`


Identifies a type of reservation affinity.

## Methods

### ReservationAffinity

`ReservationAffinity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ReservationAffinity can be used to configure a Vertex AI resource (e.g., a DeployedModel) to draw its Compute Engine resources from a Shared Reservation, or exclusively from on-demand capacity.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig.SparseEmbeddingConfig -->

# Class SparseEmbeddingConfig (1.134.0)

`SparseEmbeddingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for sparse emebdding generation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`bm25` |
Use BM25 scoring algorithm. This field is a member of `oneof` _ `model` .
|

## Classes

### Bm25

`Bm25(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message for BM25 parameters.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### SparseEmbeddingConfig

`SparseEmbeddingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for sparse emebdding generation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsPager -->

# Class ListContextsPager (1.134.0)

```
ListContextsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
provides an `__iter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListContextsPager

```
ListContextsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxInstance -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitorJob.FeatureMonitorJobTrigger -->

# Class FeatureMonitorJobTrigger (1.134.0)

`FeatureMonitorJobTrigger(value)`


Choices of the trigger type.

## Enums |
|
|---|---|
Name |
Description |
`FEATURE_MONITOR_JOB_TRIGGER_UNSPECIFIED` |
Trigger type unspecified. |
`FEATURE_MONITOR_JOB_TRIGGER_PERIODIC` |
Triggered by periodic schedule. |
`FEATURE_MONITOR_JOB_TRIGGER_ON_DEMAND` |
Triggered on demand by CreateFeatureMonitorJob request. |

## Methods

### FeatureMonitorJobTrigger

`FeatureMonitorJobTrigger(value)`


Choices of the trigger type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModalityTokenCount -->

# Class ModalityTokenCount (1.134.0)

`ModalityTokenCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents token counting info for a single modality.

## Attributes |
|
|---|---|
Name |
Description |
`modality` |
`google.cloud.aiplatform_v1.types.Modality`
The modality associated with this token count. |
`token_count` |
`int`
Number of tokens. |

## Methods

### ModalityTokenCount

`ModalityTokenCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents token counting info for a single modality.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SessionEvent -->

# Class SessionEvent (1.134.0)

`SessionEvent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An event represents a message from either the user or agent.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the event. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}/events/{event}` .
|
`author` |
`str`
Required. The name of the agent that sent the event, or user. |
`content` |
Optional. Content of the event provided by the author. |
`invocation_id` |
`str`
Required. The invocation id of the event, multiple events can have the same invocation id. |
`actions` |
Optional. Actions executed by the agent. |
`timestamp` |
`google.protobuf.timestamp_pb2.Timestamp`
Required. Timestamp when the event was created on client side. |
`error_code` |
`str`
Optional. Error code if the response is an error. Code varies by model. |
`error_message` |
`str`
Optional. Error message if the response is an error. |
`event_metadata` |
Optional. Metadata relating to this event. |

## Methods

### SessionEvent

`SessionEvent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An event represents a message from either the user or agent.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchInstance -->

# Class TrajectoryInOrderMatchInstance (1.134.0)

```
TrajectoryInOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryInOrderMatch instance.

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

### TrajectoryInOrderMatchInstance

```
TrajectoryInOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryInOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptResponse -->

# Class AugmentPromptResponse (1.134.0)

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.

## Attributes |
|
|---|---|
Name |
Description |
`augmented_prompt` |
`MutableSequence[`
Augmented prompt, only text format is supported for now. |
`facts` |
`MutableSequence[`
Retrieved facts from RAG data sources. |

## Methods

### AugmentPromptResponse

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEntityTypeOperationMetadata -->

# Class CreateEntityTypeOperationMetadata (1.134.0)

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for EntityType. |

## Methods

### CreateEntityTypeOperationMetadata

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.AutoRoutingMode -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsRequest -->

# Class ListSessionsRequest (1.134.0)

`ListSessionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.ListSessions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the location to list sessions from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`page_size` |
`int`
Optional. The maximum number of sessions to return. The service may return fewer than this value. If unspecified, at most 100 sessions will be returned. |
`page_token` |
`str`
Optional. The next_page_token value returned from a previous list SessionService.ListSessions call. |
`filter` |
`str`
Optional. The standard list filter. Supported fields: \* `display_name` \* `user_id`
Example: `display_name="abc"` , `user_id="123"` .
|
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
- `update_time`
Example: `create_time desc` .
|

## Methods

### ListSessionsRequest

`ListSessionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.ListSessions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UsageMetadata.TrafficType -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMemoryRequest -->

# Class GetMemoryRequest (1.134.0)

`GetMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.GetMemory.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Memory. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/memories/{memory}`
|

## Methods

### GetMemoryRequest

`GetMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.GetMemory.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesPager -->

# Class ListIndexesPager (1.134.0)

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

## Methods

### ListIndexesPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.RagManagedDb.ANN -->

# Class ANN (1.134.0)

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

## Attributes |
|
|---|---|
Name |
Description |
`tree_depth` |
`int`
The depth of the tree-based structure. Only depth values of 2 and 3 are supported. Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that. Default value is 2. |
`leaf_count` |
`int`
Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid. Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus). Default value is 500. |

## Methods

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseScheduleRequest -->

# Class PauseScheduleRequest (1.134.0)

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### PauseScheduleRequest

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk.Maps.PlaceAnswerSources -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessResult -->

# Class QuestionAnsweringCorrectnessResult (1.134.0)

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Correctness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering correctness score. |
`confidence` |
`float`
Output only. Confidence for question answering correctness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringCorrectnessResult

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessResult -->

# Class QuestionAnsweringHelpfulnessResult (1.134.0)

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering helpfulness score. |
`confidence` |
`float`
Output only. Confidence for question answering helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringHelpfulnessResult

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoObjectTrackingPredictionParams -->

# Class VideoObjectTrackingPredictionParams (1.134.0)

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
The Model only returns predictions with at least this confidence score. Default value is 0.0 |
`max_predictions` |
`int`
The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50. |
`min_bounding_box_size` |
`float`
Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0. |

## Methods

### VideoObjectTrackingPredictionParams

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

### VideoObjectTrackingPredictionParams

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReservationAffinity -->

# Class ReservationAffinity (1.134.0)

`ReservationAffinity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ReservationAffinity can be used to configure a Vertex AI resource (e.g., a DeployedModel) to draw its Compute Engine resources from a Shared Reservation, or exclusively from on-demand capacity.

## Attributes |
|
|---|---|
Name |
Description |
`reservation_affinity_type` |
Required. Specifies the reservation affinity type. |
`key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and
specify the name of your reservation as its value.
|
`values` |
`MutableSequence[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. |

## Classes

### Type

`Type(value)`


Identifies a type of reservation affinity.

## Methods

### ReservationAffinity

`ReservationAffinity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ReservationAffinity can be used to configure a Vertex AI resource (e.g., a DeployedModel) to draw its Compute Engine resources from a Shared Reservation, or exclusively from on-demand capacity.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.DecayCurveAutomatedStoppingSpec -->

# Class DecayCurveAutomatedStoppingSpec (1.134.0)

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if Measurement.elapsed_duration is used as the x-axis of each Trials Decay Curve. Otherwise, Measurement.step_count will be used as the x-axis. |

## Methods

### DecayCurveAutomatedStoppingSpec

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.VertexSessionSource -->

# Class VertexSessionSource (1.134.0)

`VertexSessionSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines an Agent Engine Session from which to generate the memories.
If `scope`

is not provided, the scope will be extracted from the
Session (i.e. {"user_id": sesison.user_id}).

## Attributes |
|
|---|---|
Name |
Description |
`session` |
`str`
Required. The resource name of the Session to generate memories for. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Time range to define which session events should be used to generate memories. Start time (inclusive) of the time range. If not set, the start time is unbounded. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. End time (exclusive) of the time range. If not set, the end time is unbounded. |

## Methods

### VertexSessionSource

`VertexSessionSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines an Agent Engine Session from which to generate the memories.
If `scope`

is not provided, the scope will be extracted from the
Session (i.e. {"user_id": sesison.user_id}).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsPager -->

# Class ListCustomJobsPager (1.134.0)

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

## Methods

### ListCustomJobsPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.EndpointConfig -->

# Class EndpointConfig (1.134.0)

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint_display_name` |
`str`
Optional. The user-specified display name of the endpoint. If not set, a default name will be used. |
`dedicated_endpoint_enabled` |
`bool`
Optional. Deprecated. Use dedicated_endpoint_disabled instead. If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon. |
`dedicated_endpoint_disabled` |
`bool`
Optional. By default, if dedicated endpoint is enabled and private service connect config is not set, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. If private service connect config is set, the endpoint will be exposed through private service connect. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon. If this field is set to true, the dedicated endpoint will be disabled and the deployed model will be exposed through the shared DNS {region}-aiplatform.googleapis.com. |
`private_service_connect_config` |
Optional. Configuration for private service connect. If set, the endpoint will be exposed through private service connect. |
`endpoint_user_id` |
`str`
Optional. Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The
last character must be a letter or number.
If the first character is a number, this value may be up to
9 characters, and valid characters are `[0-9]` with no
leading zeros.
When using HTTP/JSON, this field is populated based on a
query string argument, such as `?endpoint_id=12345` . This
is the fallback for fields that are not included in either
the URI or the body.
|

## Methods

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetRagFileRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service -->

# Package prediction_service (1.134.0)

API documentation for `aiplatform_v1.services.prediction_service`

package.

## Classes

[PredictionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient)

A service for online predictions and explanations.

[PredictionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient)

A service for online predictions and explanations.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeType -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelCustomJobRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.MedianAutomatedStoppingSpec -->

# Class MedianAutomatedStoppingSpec (1.134.0)

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if median automated stopping rule applies on Measurement.elapsed_duration. It means that elapsed_duration field of latest measurement of current Trial is used to compute median objective value for each completed Trials. |

## Methods

### MedianAutomatedStoppingSpec

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VideoMetadata -->

# Class VideoMetadata (1.134.0)

`VideoMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describes the input video content.

## Attributes |
|
|---|---|
Name |
Description |
`start_offset` |
`google.protobuf.duration_pb2.Duration`
Optional. The start offset of the video. |
`end_offset` |
`google.protobuf.duration_pb2.Duration`
Optional. The end offset of the video. |

## Methods

### VideoMetadata

`VideoMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describes the input video content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient -->

# Class FeaturestoreServiceClient (1.134.0)

```
FeaturestoreServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that handles CRUD and List for resources for Featurestore.

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
`FeaturestoreServiceTransport` |
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

### FeaturestoreServiceClient

```
FeaturestoreServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the featurestore service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeaturestoreServiceTransport,Callable[..., FeaturestoreServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeaturestoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_create_features

```
batch_create_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.BatchCreateFeaturesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.featurestore_service.CreateFeatureRequest
]
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


Creates a batch of Features in a given EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_create_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_batch_create_features)(request=request)
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
The request object. Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures. |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: |
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The |
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

### batch_read_feature_values

```
batch_read_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.BatchReadFeatureValuesRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[str] = None,
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


Batch reads Feature values from a Featurestore.

This API enables batch reading Feature values, where each read instance in the batch may read Feature values of entities from one or more EntityTypes. Point-in-time correctness is guaranteed for Feature values of each read instance as of each instance's read timestamp.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_read_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
csv_read_instances = aiplatform_v1.[CsvSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CsvSource.html)()
csv_read_instances.gcs_source.uris = ['uris_value1', 'uris_value2']
destination = aiplatform_v1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
entity_type_specs = aiplatform_v1.[EntityTypeSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.EntityTypeSpec.html)()
entity_type_specs.entity_type_id = "entity_type_id_value"
entity_type_specs.feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1.[BatchReadFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.html)(
csv_read_instances=csv_read_instances,
featurestore="featurestore_value",
destination=destination,
entity_type_specs=entity_type_specs,
)
# Make the request
operation = client.[batch_read_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_batch_read_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.BatchReadFeatureValues. |
`featurestore` |
`str`
Required. The resource name of the Featurestore from which to query Feature values. Format: |
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

### create_entity_type

```
create_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.CreateEntityTypeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
entity_type: typing.Optional[
google.cloud.aiplatform_v1.types.entity_type.EntityType
] = None,
entity_type_id: typing.Optional[str] = None,
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


Creates a new EntityType in a given Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEntityTypeRequest.html)(
parent="parent_value",
entity_type_id="entity_type_id_value",
)
# Make the request
operation = client.[create_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_create_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.CreateEntityType. |
`parent` |
`str`
Required. The resource name of the Featurestore to create EntityTypes. Format: |
`entity_type` |
The EntityType to create. This corresponds to the |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
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

### create_feature

```
create_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.CreateFeatureRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature: typing.Optional[google.cloud.aiplatform_v1.types.feature.Feature] = None,
feature_id: typing.Optional[str] = None,
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


Creates a new Feature in a given EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_create_feature)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature. |
`parent` |
`str`
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: |
`feature` |
Required. The Feature to create. This corresponds to the |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are |
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

### create_featurestore

```
create_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.CreateFeaturestoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
featurestore: typing.Optional[
google.cloud.aiplatform_v1.types.featurestore.Featurestore
] = None,
featurestore_id: typing.Optional[str] = None,
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


Creates a new Featurestore in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeaturestoreRequest.html)(
parent="parent_value",
featurestore_id="featurestore_id_value",
)
# Make the request
operation = client.[create_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_create_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeaturestore. |
`parent` |
`str`
Required. The resource name of the Location to create Featurestores. Format: |
`featurestore` |
Required. The Featurestore to create. This corresponds to the |
`featurestore_id` |
`str`
Required. The ID to use for this Featurestore, which will become the final component of the Featurestore's resource name. This value may be up to 60 characters, and valid characters are |
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

### delete_entity_type

```
delete_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteEntityTypeRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
force: typing.Optional[bool] = None,
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


Deletes a single EntityType. The EntityType must not have any
Features or `force`

must be set to true for the request to
succeed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEntityTypeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteEntityType. |
`name` |
`str`
Required. The name of the EntityType to be deleted. Format: |
`force` |
`bool`
If set to true, any Features for this EntityType will also be deleted. (Otherwise, the request will only work if the EntityType has no Features.) This corresponds to the |
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

### delete_feature

```
delete_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteFeatureRequest,
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


Deletes a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_feature)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature. |
`name` |
`str`
Required. The name of the Features to be deleted. Format: |
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

### delete_feature_values

```
delete_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Delete Feature values from Featurestore.

The progress of the deletion is tracked by the returned operation. The deleted feature values are guaranteed to be invisible to subsequent read operations after the operation is marked as successfully done.

If a delete feature values operation fails, the feature values returned from reads and exports may be inconsistent. If consistency is required, the caller must retry the same delete request again and wait till the new operation returned is marked as successfully done.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
select_entity = aiplatform_v1.SelectEntity()
select_entity.entity_id_selector.csv_source.gcs_source.uris = ['uris_value1', 'uris_value2']
request = aiplatform_v1.[DeleteFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest.html)(
select_entity=select_entity,
entity_type="entity_type_value",
)
# Make the request
operation = client.[delete_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeatureValues. |
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: |
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

### delete_featurestore

```
delete_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteFeaturestoreRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
force: typing.Optional[bool] = None,
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


Deletes a single Featurestore. The Featurestore must not contain
any EntityTypes or `force`

must be set to true for the request
to succeed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeaturestore. |
`name` |
`str`
Required. The name of the Featurestore to be deleted. Format: |
`force` |
`bool`
If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.) This corresponds to the |
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

### entity_type_path

```
entity_type_path(
project: str, location: str, featurestore: str, entity_type: str
) -> str
```


Returns a fully-qualified entity_type string.

### export_feature_values

```
export_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ExportFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Exports Feature values from all the entities of a target EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_export_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
feature_selector = aiplatform_v1.[FeatureSelector](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureSelector.html)()
feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1.[ExportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest.html)(
entity_type="entity_type_value",
destination=destination,
feature_selector=feature_selector,
)
# Make the request
operation = client.[export_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_export_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ExportFeatureValues. |
`entity_type` |
`str`
Required. The resource name of the EntityType from which to export Feature values. Format: |
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

### feature_path

```
feature_path(
project: str, location: str, featurestore: str, entity_type: str, feature: str
) -> str
```


Returns a fully-qualified feature string.

### featurestore_path

`featurestore_path(project: str, location: str, featurestore: str) -> str`


Returns a fully-qualified featurestore string.

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
`FeaturestoreServiceClient` |
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
`FeaturestoreServiceClient` |
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
`FeaturestoreServiceClient` |
The constructed client. |

### get_entity_type

```
get_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.GetEntityTypeRequest,
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
) -> google.cloud.aiplatform_v1.types.entity_type.EntityType
```


Gets details of a single EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEntityTypeRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_get_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.GetEntityType. |
`name` |
`str`
Required. The name of the EntityType resource. Format: |
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
An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver. |

### get_feature

```
get_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.GetFeatureRequest,
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
) -> google.cloud.aiplatform_v1.types.feature.Feature
```


Gets details of a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_get_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature. |
`name` |
`str`
Required. The name of the Feature resource. Format for entity_type as parent: |
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
Feature Metadata information. For example, color is a feature that describes an apple. |

### get_featurestore

```
get_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.GetFeaturestoreRequest,
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
) -> google.cloud.aiplatform_v1.types.featurestore.Featurestore
```


Gets details of a single Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_get_featurestore)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.GetFeaturestore. |
`name` |
`str`
Required. The name of the Featurestore resource. This corresponds to the |
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
Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values. |

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

### import_feature_values

```
import_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ImportFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Imports Feature values into the Featurestore from a source storage. The progress of the import is tracked by the returned operation. The imported features are guaranteed to be visible to subsequent read operations after the operation is marked as successfully done.

If an import operation fails, the Feature values returned from reads and exports may be inconsistent. If consistency is required, the caller must retry the same import request again and wait till the new operation returned is marked as successfully done.

There are also scenarios where the caller can cause inconsistency.

- Source data for import contains multiple distinct Feature values for the same entity ID and timestamp.
- Source is modified during an import. This includes adding, updating, or removing source data and/or metadata. Examples of updating metadata include but are not limited to changing storage location, storage class, or retention policy.
- Online serving cluster is under-provisioned.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_import_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
avro_source = aiplatform_v1.[AvroSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AvroSource.html)()
avro_source.gcs_source.uris = ['uris_value1', 'uris_value2']
feature_specs = aiplatform_v1.[FeatureSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesRequest.FeatureSpec.html)()
feature_specs.id = "id_value"
request = aiplatform_v1.[ImportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesRequest.html)(
avro_source=avro_source,
feature_time_field="feature_time_field_value",
entity_type="entity_type_value",
feature_specs=feature_specs,
)
# Make the request
operation = client.[import_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_import_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ImportFeatureValues. |
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: |
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

### list_entity_types

```
list_entity_types(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
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
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesPager
)
```


Lists EntityTypes in a given Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_entity_types():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEntityTypesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_entity_types](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_list_entity_types)(request=request)
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
The request object. Request message for FeaturestoreService.ListEntityTypes. |
`parent` |
`str`
Required. The resource name of the Featurestore to list EntityTypes. Format: |
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
Response message for FeaturestoreService.ListEntityTypes. Iterating over this object will yield results and resolve additional pages automatically. |

### list_features

```
list_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
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
) -> google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesPager
```


Lists Features in a given EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_list_features)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures. |
`parent` |
`str`
Required. The resource name of the Location to list Features. Format for entity_type as parent: |
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
Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures. Iterating over this object will yield results and resolve additional pages automatically. |

### list_featurestores

```
list_featurestores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
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
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresPager
)
```


Lists Featurestores in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_featurestores():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturestoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_featurestores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_list_featurestores)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeaturestores. |
`parent` |
`str`
Required. The resource name of the Location to list Featurestores. Format: |
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
Response message for FeaturestoreService.ListFeaturestores. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_entity_type_path

`parse_entity_type_path(path: str) -> typing.Dict[str, str]`


Parses a entity_type path into its component segments.

### parse_feature_path

`parse_feature_path(path: str) -> typing.Dict[str, str]`


Parses a feature path into its component segments.

### parse_featurestore_path

`parse_featurestore_path(path: str) -> typing.Dict[str, str]`


Parses a featurestore path into its component segments.

### search_features

```
search_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
dict,
]
] = None,
*,
location: typing.Optional[str] = None,
query: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesPager
)
```


Searches Features matching a query in a given project.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_search_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesRequest.html)(
location="location_value",
)
# Make the request
page_result = client.[search_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_search_features)(request=request)
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
The request object. Request message for FeaturestoreService.SearchFeatures. |
`location` |
`str`
Required. The resource name of the Location to search Features. Format: |
`query` |
`str`
Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using |
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
Response message for FeaturestoreService.SearchFeatures. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_entity_type

```
update_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.UpdateEntityTypeRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[
google.cloud.aiplatform_v1.types.entity_type.EntityType
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
) -> google.cloud.aiplatform_v1.types.entity_type.EntityType
```


Updates the parameters of a single EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEntityTypeRequest.html)(
)
# Make the request
response = client.[update_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_update_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.UpdateEntityType. |
`entity_type` |
Required. The EntityType's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver. |

### update_feature

```
update_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.UpdateFeatureRequest,
dict,
]
] = None,
*,
feature: typing.Optional[google.cloud.aiplatform_v1.types.feature.Feature] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.feature.Feature
```


Updates the parameters of a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureRequest.html)(
)
# Make the request
response = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_update_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature. |
`feature` |
Required. The Feature's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
Feature Metadata information. For example, color is a feature that describes an apple. |

### update_featurestore

```
update_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.UpdateFeaturestoreRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[
google.cloud.aiplatform_v1.types.featurestore.Featurestore
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


Updates the parameters of a single Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeaturestoreRequest.html)(
)
# Make the request
operation = client.[update_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_update_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.UpdateFeaturestore. |
`featurestore` |
Required. The Featurestore's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesPager -->

# Class ListStudiesPager (1.134.0)

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse) object, and
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

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListStudiesPager

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.NumericFilter -->

# Class NumericFilter (1.134.0)

`NumericFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: "a" value_int: 42} {name: "b" value_float: 1.0} Database Point 1: {name: "a" value_int: 10} {name: "b" value_float: 2.0} Database Point 2: {name: "a" value_int: -1} {name: "b" value_float: 3.0} Query: {name: "a" value_int: 12 operator: LESS} // Matches Point 1, 2 {name: "b" value_float: 2.0 operator: EQUAL} // Matches Point 1

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
`value_int` |
`int`
int value type. This field is a member of `oneof` _ `Value` .
|
`value_float` |
`float`
float value type. This field is a member of `oneof` _ `Value` .
|
`value_double` |
`float`
double value type. This field is a member of `oneof` _ `Value` .
|
`name` |
`str`
Required. Column name in BigQuery that used as filters. |
`op` |
Optional. This MUST be specified for queries and must NOT be specified for database points. This field is a member of `oneof` _ `_op` .
|

## Classes

### Operator

`Operator(value)`


Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

## Methods

### NumericFilter

`NumericFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: "a" value_int: 42} {name: "b" value_float: 1.0} Database Point 1: {name: "a" value_int: 10} {name: "b" value_float: 2.0} Database Point 2: {name: "a" value_int: -1} {name: "b" value_float: 3.0} Query: {name: "a" value_int: 12 operator: LESS} // Matches Point 1, 2 {name: "b" value_float: 2.0 operator: EQUAL} // Matches Point 1

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ThresholdConfig -->

# Class ThresholdConfig (1.134.0)

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Specify a threshold value that can trigger the alert. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature. This field is a member of `oneof` _ `threshold` .
|

## Methods

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchInstance -->

# Class TrajectoryAnyOrderMatchInstance (1.134.0)

```
TrajectoryAnyOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryAnyOrderMatch instance.

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

### TrajectoryAnyOrderMatchInstance

```
TrajectoryAnyOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryAnyOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsPager -->

# Class ListDataItemsPager (1.134.0)

```
ListDataItemsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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


A pager for iterating through `list_data_items`

requests.

This class thinly wraps an initial
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_items`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDataItems`

requests and continue to iterate
through the `data_items`

field on the
corresponding responses.

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataItemsPager

```
ListDataItemsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSessionRequest -->

# Class GetSessionRequest (1.134.0)

`GetSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.GetSession.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the session. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|

## Methods

### GetSessionRequest

`GetSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.GetSession.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.DeployVertex -->

# Class DeployVertex (1.134.0)

`DeployVertex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Multiple setups to deploy the PublisherModel.

## Attribute |
|
|---|---|
Name |
Description |
`multi_deploy_vertex` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy]`
Optional. One click deployment configurations. |

## Methods

### DeployVertex

`DeployVertex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Multiple setups to deploy the PublisherModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample.SearchKeyGenerationMethod -->

# Class SearchKeyGenerationMethod (1.134.0)

`SearchKeyGenerationMethod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options for generating the search key from the conversation history.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`last_entry` |
Use only the last entry of the conversation history ( `contents_example.contents` ) as the search key.
This field is a member of `oneof` _ `method` .
|

## Classes

### LastEntry

`LastEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for using only the last entry of the conversation history as the search key.

## Methods

### SearchKeyGenerationMethod

`SearchKeyGenerationMethod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options for generating the search key from the conversation history.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.IndexConfig.DistanceMeasureType -->

# Class DistanceMeasureType (1.134.0)

`DistanceMeasureType(value)`


The distance measure used in nearest neighbor search.

```
We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.
```


## Enums |
|
|---|---|
Name |
Description |
`DISTANCE_MEASURE_TYPE_UNSPECIFIED` |
Should not be set. |
`SQUARED_L2_DISTANCE` |
Euclidean (L_2) Distance. |
`COSINE_DISTANCE` |
Cosine Distance. Defined as 1 - cosine similarity. |

## Methods

### DistanceMeasureType

`DistanceMeasureType(value)`


The distance measure used in nearest neighbor search.

```
We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.
```

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/multiprocessing -->

# Multiprocessing

**NOTE**: Because this client uses [ grpc](https://grpc.github.io/grpc/python/grpc.html#module-grpc) library, it is safe to
share instances across threads. In multiprocessing scenarios, the best
practice is to create client instances

*after*the invocation of

[by](https://docs.python.org/3/library/os.html#os.fork)

`os.fork()`

[or](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.pool.Pool)

`multiprocessing.pool.Pool`

[.](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Process)

`multiprocessing.Process`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service -->

# Package vertex_rag_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.vertex_rag_service`

package.

## Classes

[VertexRagServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient)

A service for retrieving relevant contexts.

[VertexRagServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceClient)

A service for retrieving relevant contexts.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsPager -->

# Class ListEventsPager (1.134.0)

```
ListEventsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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


A pager for iterating through `list_events`

requests.

This class thinly wraps an initial
[ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse) object, and
provides an `__iter__`

method to iterate through its
`session_events`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEvents`

requests and continue to iterate
through the `session_events`

field on the
corresponding responses.

All the usual [ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEventsPager

```
ListEventsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsPager -->

# Class ListEndpointsPager (1.134.0)

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

## Methods

### ListEndpointsPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesPager -->

# Class ListSchedulesPager (1.134.0)

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

## Methods

### ListSchedulesPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsPager -->

# Class ListArtifactsPager (1.134.0)

```
ListArtifactsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
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


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse) object, and
provides an `__iter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListArtifactsPager

```
ListArtifactsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingPredictResponse -->

# Class StreamingPredictResponse (1.134.0)

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.

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

### StreamingPredictResponse

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetOperationMetadata -->

# Class CreateDatasetOperationMetadata (1.134.0)

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDatasetOperationMetadata

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionCall -->

# Class FunctionCall (1.134.0)

`FunctionCall(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing the parameters and their values.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Optional. The name of the function to call. Matches [FunctionDeclaration.name]. |
`args` |
`google.protobuf.struct_pb2.Struct`
Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details. |
`partial_args` |
`MutableSequence[`
Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. |
`will_continue` |
`bool`
Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. |

## Methods

### FunctionCall

`FunctionCall(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing the parameters and their values.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPipelineJobRequest -->

# Class GetPipelineJobRequest (1.134.0)

`GetPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetPipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### GetPipelineJobRequest

`GetPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetPipelineJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptResponse -->

# Class AugmentPromptResponse (1.134.0)

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.

## Attributes |
|
|---|---|
Name |
Description |
`augmented_prompt` |
`MutableSequence[`
Augmented prompt, only text format is supported for now. |
`facts` |
`MutableSequence[`
Retrieved facts from RAG data sources. |

## Methods

### AugmentPromptResponse

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.MedianAutomatedStoppingSpec -->

# Class MedianAutomatedStoppingSpec (1.134.0)

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if median automated stopping rule applies on Measurement.elapsed_duration. It means that elapsed_duration field of latest measurement of current Trial is used to compute median objective value for each completed Trials. |

## Methods

### MedianAutomatedStoppingSpec

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ThresholdConfig -->

# Class ThresholdConfig (1.134.0)

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Specify a threshold value that can trigger the alert. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature. This field is a member of `oneof` _ `threshold` .
|

## Methods

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeOperationMetadata -->

# Class CreateEntityTypeOperationMetadata (1.134.0)

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for EntityType. |

## Methods

### CreateEntityTypeOperationMetadata

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseScheduleRequest -->

# Class PauseScheduleRequest (1.134.0)

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### PauseScheduleRequest

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFile -->

# Class RagFile (1.134.0)

`RagFile(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagFile contains user data for chunking, embedding and indexing.

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
Output only. Google Cloud Storage location of the RagFile. It does not support wildcards in the Cloud Storage uri for now. This field is a member of `oneof` _ `rag_file_source` .
|
`google_drive_source` |
Output only. Google Drive location. Supports importing individual files as well as Google Drive folders. This field is a member of `oneof` _ `rag_file_source` .
|
`direct_upload_source` |
Output only. The RagFile is encapsulated and uploaded in the UploadRagFile request. This field is a member of `oneof` _ `rag_file_source` .
|
`slack_source` |
The RagFile is imported from a Slack channel. This field is a member of `oneof` _ `rag_file_source` .
|
`jira_source` |
The RagFile is imported from a Jira query. This field is a member of `oneof` _ `rag_file_source` .
|
`share_point_sources` |
The RagFile is imported from a SharePoint source. This field is a member of `oneof` _ `rag_file_source` .
|
`name` |
`str`
Output only. The resource name of the RagFile. |
`display_name` |
`str`
Required. The display name of the RagFile. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the RagFile. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was last updated. |
`file_status` |
Output only. State of the RagFile. |

## Methods

### RagFile

`RagFile(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagFile contains user data for chunking, embedding and indexing.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoObjectTrackingPredictionParams -->

# Class VideoObjectTrackingPredictionParams (1.134.0)

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
The Model only returns predictions with at least this confidence score. Default value is 0.0 |
`max_predictions` |
`int`
The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50. |
`min_bounding_box_size` |
`float`
Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0. |

## Methods

### VideoObjectTrackingPredictionParams

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

### VideoObjectTrackingPredictionParams

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.IndexConfig.DistanceMeasureType -->

# Class DistanceMeasureType (1.134.0)

`DistanceMeasureType(value)`


The distance measure used in nearest neighbor search.

```
We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.
```


## Enums |
|
|---|---|
Name |
Description |
`DISTANCE_MEASURE_TYPE_UNSPECIFIED` |
Should not be set. |
`SQUARED_L2_DISTANCE` |
Euclidean (L_2) Distance. |
`COSINE_DISTANCE` |
Cosine Distance. Defined as 1 - cosine similarity. |

## Methods

### DistanceMeasureType

`DistanceMeasureType(value)`


The distance measure used in nearest neighbor search.

```
We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelOperationMetadata -->

# Class UndeployModelOperationMetadata (1.134.0)

```
UndeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UndeployModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UndeployModelOperationMetadata

```
UndeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UndeployModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationVerbosityInput -->

# Class SummarizationVerbosityInput (1.134.0)

`SummarizationVerbosityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization verbosity metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization verbosity score metric. |
`instance` |
Required. Summarization verbosity instance. |

## Methods

### SummarizationVerbosityInput

`SummarizationVerbosityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization verbosity metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchSpec -->

# Class TrajectoryExactMatchSpec (1.134.0)

`TrajectoryExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.

## Methods

### TrajectoryExactMatchSpec

`TrajectoryExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.BigtableMetadata -->

# Class BigtableMetadata (1.134.0)

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.

## Attribute |
|
|---|---|
Name |
Description |
`read_app_profile` |
`str`
The Bigtable App Profile to use for reading from Bigtable. |

## Methods

### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob -->

# Class CustomContainerTrainingJob (1.134.0)

```
CustomContainerTrainingJob(
display_name: str,
container_uri: str,
command: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_image_uri: typing.Optional[str] = None,
model_serving_container_predict_route: typing.Optional[str] = None,
model_serving_container_health_route: typing.Optional[str] = None,
model_serving_container_command: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_args: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
model_serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
model_description: typing.Optional[str] = None,
model_instance_schema_uri: typing.Optional[str] = None,
model_parameters_schema_uri: typing.Optional[str] = None,
model_prediction_schema_uri: typing.Optional[str] = None,
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
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
)
```


Class to launch a Custom Training Job in Vertex AI using a Container.

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

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
`CustomTrainingJob`

should be peered.

Specify the name of the network using the format
`projects/{project}/global/networks/{network}`

. Replace {project} with
the project number, such as `12345`

, and {network} with a network name.

Before specifying a network, private services access must be configured for the network. If private services access isn't configured, then the custom training job can't be peered with a network.

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

### web_access_uris

Returns the URIs used to access the custom training job.

## Methods

### CustomContainerTrainingJob

```
CustomContainerTrainingJob(
display_name: str,
container_uri: str,
command: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_image_uri: typing.Optional[str] = None,
model_serving_container_predict_route: typing.Optional[str] = None,
model_serving_container_health_route: typing.Optional[str] = None,
model_serving_container_command: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_args: typing.Optional[typing.Sequence[str]] = None,
model_serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
model_serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
model_description: typing.Optional[str] = None,
model_instance_schema_uri: typing.Optional[str] = None,
model_parameters_schema_uri: typing.Optional[str] = None,
model_prediction_schema_uri: typing.Optional[str] = None,
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
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
)
```


Constructs a Custom Container Training Job.

job = aiplatform.CustomContainerTrainingJob( display_name='test-train', container_uri='gcr.io/my_project_id/my_image_name:tag', command=['python3', 'run_script.py'] model_serving_container_image_uri='gcr.io/my-trainer/serving:1', model_serving_container_predict_route='predict', model_serving_container_health_route='metadata, labels={'key': 'value'}, )

Usage with Dataset:

ds = aiplatform.TabularDataset( 'projects/my-project/locations/us-central1/datasets/12345')

job.run( ds, replica_count=1, model_display_name='my-trained-model', model_labels={'key': 'value'}, )

Usage without Dataset:

job.run(replica_count=1, model_display_name='my-trained-model)

To ensure your model gets saved in Vertex AI, write your saved model to os.environ["AIP_MODEL_DIR"] in your provided training script.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`container_uri` |
`str`
Required: Uri of the training container image in the GCR. |
`command` |
`Sequence[str]`
The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided |
`model_serving_container_image_uri` |
`str`
If the training produces a managed Vertex AI Model, the URI of the Model serving container suitable for serving the model produced by the training script. |
`model_serving_container_predict_route` |
`str`
If the training produces a managed Vertex AI Model, An HTTP path to send prediction requests to the container, and which must be supported by it. If not specified a default HTTP path will be used by Vertex AI. |
`model_serving_container_health_route` |
`str`
If the training produces a managed Vertex AI Model, an HTTP path to send health check requests to the container, and which must be supported by it. If not specified a standard HTTP path will be used by AI Platform. |
`model_serving_container_command` |
`Sequence[str]`
The command with which the container is run. Not executed within a shell. The Docker image's ENTRYPOINT is used if this is not provided. Variable references $(VAR_NAME) are expanded using the container's environment. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |
`model_serving_container_args` |
`Sequence[str]`
The arguments to the command. The Docker image's CMD is used if this is not provided. Variable references $(VAR_NAME) are expanded using the container's environment. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |
`model_serving_container_environment_variables` |
`Dict[str, str]`
The environment variables that are to be present in the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. |
`model_serving_container_ports` |
`Sequence[int]`
Declaration of ports that are exposed by the container. This field is primarily informational, it gives Vertex AI information about the network connections the container uses. Listing or not a port here has no impact on whether the port is actually exposed, any port listening on the default "0.0.0.0" address inside a container will be accessible from the network. |
`model_description` |
`str`
The description of the Model. |
`model_instance_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in |
`model_parameters_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via |
`model_prediction_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via |
`explanation_metadata` |
`explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`project` |
`str`
Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`staging_bucket` |
`str`
Bucket used to stage source and training artifacts. Overrides staging_bucket set in aiplatform.init. |

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
dataset: typing.Optional[
typing.Union[
google.cloud.aiplatform.datasets.image_dataset.ImageDataset,
google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset,
google.cloud.aiplatform.datasets.text_dataset.TextDataset,
google.cloud.aiplatform.datasets.video_dataset.VideoDataset,
]
] = None,
annotation_schema_uri: typing.Optional[str] = None,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
base_output_dir: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
bigquery_destination: typing.Optional[str] = None,
args: typing.Optional[typing.List[typing.Union[str, float, int]]] = None,
environment_variables: typing.Optional[typing.Dict[str, str]] = None,
replica_count: int = 1,
machine_type: str = "n1-standard-4",
accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
accelerator_count: int = 0,
boot_disk_type: str = "pd-ssd",
boot_disk_size_gb: int = 100,
reduction_server_replica_count: int = 0,
reduction_server_machine_type: typing.Optional[str] = None,
reduction_server_container_uri: typing.Optional[str] = None,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
training_filter_split: typing.Optional[str] = None,
validation_filter_split: typing.Optional[str] = None,
test_filter_split: typing.Optional[str] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
enable_dashboard_access: bool = False,
tensorboard: typing.Optional[str] = None,
sync=True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
reservation_affinity_type: typing.Optional[
typing.Literal["NO_RESERVATION", "ANY_RESERVATION", "SPECIFIC_RESERVATION"]
] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None,
) -> typing.Optional[google.cloud.aiplatform.models.Model]
```


Runs the custom training job.

Distributed Training Support: If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. ie: replica_count = 10 will result in 1 chief and 9 workers All replicas have same machine_type, accelerator_type, and accelerator_count

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
Data filter splits:
Assigns input data to training, validation, and test sets
based on the given filters, data pieces not matched by any
filter are ignored. Currently only supported for Datasets
containing DataItems.
If any of the filters in this message are to match nothing, then
they can be set as '-' (the minus sign).
If using filter splits, all of `training_filter_split`, `validation_filter_split` and
`test_filter_split` must be provided.
Supported only for unstructured Datasets.
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
`Union[datasets.ImageDataset,datasets.TabularDataset,datasets.TextDataset,datasets.VideoDataset]`
Vertex AI to fit this training against. Custom training script should retrieve datasets through passed in environment variables uris: os.environ["AIP_TRAINING_DATA_URI"] os.environ["AIP_VALIDATION_DATA_URI"] os.environ["AIP_TEST_DATA_URI"] Additionally the dataset format is passed in as: os.environ["AIP_DATA_FORMAT"] |
`annotation_schema_uri` |
`str`
Google Cloud Storage URI points to a YAML file describing annotation schema. The schema is defined as an OpenAPI 3.0.2 |
`model_display_name` |
`str`
If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
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
`base_output_dir` |
`str`
GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. Vertex AI sets the following environment variables when it runs your training code: - AIP_MODEL_DIR: a Cloud Storage URI of a directory intended for saving model artifacts, i.e. <base_output_dir>/model/ - AIP_CHECKPOINT_DIR: a Cloud Storage URI of a directory intended for saving checkpoints, i.e. <base_output_dir>/checkpoints/ - AIP_TENSORBOARD_LOG_DIR: a Cloud Storage URI of a directory intended for saving TensorBoard logs, i.e. <base_output_dir>/logs/ |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`bigquery_destination` |
`str`
Provide this field if |
`args` |
`List[Unions[str, int, float]]`
Command line arguments to be passed to the Python script. |
`environment_variables` |
`Dict[str, str]`
Environment variables to be passed to the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. At most 10 environment variables can be specified. The Name of the environment variable must be unique. environment_variables = { 'MY_KEY': 'MY_VALUE' } |
`replica_count` |
`int`
The number of worker replicas. If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. |
`machine_type` |
`str`
The type of machine to use for training. |
`accelerator_type` |
`str`
Hardware accelerator type. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
The number of accelerators to attach to a worker replica. |
`boot_disk_type` |
`str`
Type of the boot disk, default is |
`boot_disk_size_gb` |
`int`
Size in GB of the boot disk, default is 100GB. boot disk size must be within the range of [100, 64000]. |
`reduction_server_replica_count` |
`int`
The number of reduction server replicas, default is 0. |
`reduction_server_machine_type` |
`str`
Optional. The type of machine to use for reduction server. |
`reduction_server_container_uri` |
`str`
Optional. The Uri of the reduction server container image. See details: |
`training_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to train the Model. This is ignored if Dataset is not provided. |
`validation_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to validate the Model. This is ignored if Dataset is not provided. |
`test_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to evaluate the Model. This is ignored if Dataset is not provided. |
`training_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`validation_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`test_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`enable_dashboard_access` |
`bool`
Whether you want Vertex AI to enable access to the customized dashboard to training containers. |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`tpu_topology` |
`str`
Optional. Specifies the tpu topology to be used for TPU training job. This field is required for TPU v5 versions. For details on the TPU topology, refer to |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`reservation_affinity_type` |
`str`
Optional. The type of reservation affinity. One of: * "NO_RESERVATION" : No reservation is used. * "ANY_RESERVATION" : Any reservation that matches machine spec can be used. * "SPECIFIC_RESERVATION" : A specific reservation must be use used. See reservation_affinity_key and reservation_affinity_values for how to specify the reservation. |
`reservation_affinity_key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use |
`reservation_affinity_values` |
`List[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. Format: 'projects/{project_id_or_number}/zones/{zone}/reservations/{reservation_name}' |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 30 minutes. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run, staging_bucket has not been set, or model_display_name was provided but required arguments were not provided in constructor. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

### submit

```
submit(
dataset: typing.Optional[
typing.Union[
google.cloud.aiplatform.datasets.image_dataset.ImageDataset,
google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset,
google.cloud.aiplatform.datasets.text_dataset.TextDataset,
google.cloud.aiplatform.datasets.video_dataset.VideoDataset,
]
] = None,
annotation_schema_uri: typing.Optional[str] = None,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
base_output_dir: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
bigquery_destination: typing.Optional[str] = None,
args: typing.Optional[typing.List[typing.Union[str, float, int]]] = None,
environment_variables: typing.Optional[typing.Dict[str, str]] = None,
replica_count: int = 1,
machine_type: str = "n1-standard-4",
accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
accelerator_count: int = 0,
boot_disk_type: str = "pd-ssd",
boot_disk_size_gb: int = 100,
reduction_server_replica_count: int = 0,
reduction_server_machine_type: typing.Optional[str] = None,
reduction_server_container_uri: typing.Optional[str] = None,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
training_filter_split: typing.Optional[str] = None,
validation_filter_split: typing.Optional[str] = None,
test_filter_split: typing.Optional[str] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
enable_dashboard_access: bool = False,
tensorboard: typing.Optional[str] = None,
sync=True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
reservation_affinity_type: typing.Optional[
typing.Literal["NO_RESERVATION", "ANY_RESERVATION", "SPECIFIC_RESERVATION"]
] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None,
) -> typing.Optional[google.cloud.aiplatform.models.Model]
```


Submits the custom training job without blocking until completion.

Distributed Training Support: If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. ie: replica_count = 10 will result in 1 chief and 9 workers All replicas have same machine_type, accelerator_type, and accelerator_count

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
Data filter splits:
Assigns input data to training, validation, and test sets
based on the given filters, data pieces not matched by any
filter are ignored. Currently only supported for Datasets
containing DataItems.
If any of the filters in this message are to match nothing, then
they can be set as '-' (the minus sign).
If using filter splits, all of `training_filter_split`, `validation_filter_split` and
`test_filter_split` must be provided.
Supported only for unstructured Datasets.
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
`Union[datasets.ImageDataset,datasets.TabularDataset,datasets.TextDataset,datasets.VideoDataset]`
Vertex AI to fit this training against. Custom training script should retrieve datasets through passed in environment variables uris: os.environ["AIP_TRAINING_DATA_URI"] os.environ["AIP_VALIDATION_DATA_URI"] os.environ["AIP_TEST_DATA_URI"] Additionally the dataset format is passed in as: os.environ["AIP_DATA_FORMAT"] |
`annotation_schema_uri` |
`str`
Google Cloud Storage URI points to a YAML file describing annotation schema. The schema is defined as an OpenAPI 3.0.2 |
`model_display_name` |
`str`
If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
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
`base_output_dir` |
`str`
GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. Vertex AI sets the following environment variables when it runs your training code: - AIP_MODEL_DIR: a Cloud Storage URI of a directory intended for saving model artifacts, i.e. <base_output_dir>/model/ - AIP_CHECKPOINT_DIR: a Cloud Storage URI of a directory intended for saving checkpoints, i.e. <base_output_dir>/checkpoints/ - AIP_TENSORBOARD_LOG_DIR: a Cloud Storage URI of a directory intended for saving TensorBoard logs, i.e. <base_output_dir>/logs/ |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`bigquery_destination` |
`str`
Provide this field if |
`args` |
`List[Unions[str, int, float]]`
Command line arguments to be passed to the Python script. |
`environment_variables` |
`Dict[str, str]`
Environment variables to be passed to the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. At most 10 environment variables can be specified. The Name of the environment variable must be unique. environment_variables = { 'MY_KEY': 'MY_VALUE' } |
`replica_count` |
`int`
The number of worker replicas. If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. |
`machine_type` |
`str`
The type of machine to use for training. |
`accelerator_type` |
`str`
Hardware accelerator type. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
The number of accelerators to attach to a worker replica. |
`boot_disk_type` |
`str`
Type of the boot disk, default is |
`boot_disk_size_gb` |
`int`
Size in GB of the boot disk, default is 100GB. boot disk size must be within the range of [100, 64000]. |
`reduction_server_replica_count` |
`int`
The number of reduction server replicas, default is 0. |
`reduction_server_machine_type` |
`str`
Optional. The type of machine to use for reduction server. |
`reduction_server_container_uri` |
`str`
Optional. The Uri of the reduction server container image. See details: |
`training_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to train the Model. This is ignored if Dataset is not provided. |
`validation_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to validate the Model. This is ignored if Dataset is not provided. |
`test_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to evaluate the Model. This is ignored if Dataset is not provided. |
`training_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`validation_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`test_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`enable_dashboard_access` |
`bool`
Whether you want Vertex AI to enable access to the customized dashboard to training containers. |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`tpu_topology` |
`str`
Optional. Specifies the tpu topology to be used for TPU training job. This field is required for TPU v5 versions. For details on the TPU topology, refer to |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`reservation_affinity_type` |
`str`
Optional. The type of reservation affinity. One of: * "NO_RESERVATION" : No reservation is used. * "ANY_RESERVATION" : Any reservation that matches machine spec can be used. * "SPECIFIC_RESERVATION" : A specific reservation must be use used. See reservation_affinity_key and reservation_affinity_values for how to specify the reservation. |
`reservation_affinity_key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use |
`reservation_affinity_values` |
`List[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. Format: 'projects/{project_id_or_number}/zones/{zone}/reservations/{reservation_name}' |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 30 minutes. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run, staging_bucket has not been set, or model_display_name was provided but required arguments were not provided in constructor. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJobView -->

# Class NotebookExecutionJobView (1.134.0)

`NotebookExecutionJobView(value)`


Views for Get/List NotebookExecutionJob

## Enums |
|
|---|---|
Name |
Description |
`NOTEBOOK_EXECUTION_JOB_VIEW_UNSPECIFIED` |
When unspecified, the API defaults to the BASIC view. |
`NOTEBOOK_EXECUTION_JOB_VIEW_BASIC` |
Includes all fields except for direct notebook inputs. |
`NOTEBOOK_EXECUTION_JOB_VIEW_FULL` |
Includes all fields. |

## Methods

### NotebookExecutionJobView

`NotebookExecutionJobView(value)`


Views for Get/List NotebookExecutionJob

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetContextRequest -->

# Class GetContextRequest (1.134.0)

`GetContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetContext.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Context to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|

## Methods

### GetContextRequest

`GetContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetContext.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig -->

# Class PipelineTaskRerunConfig (1.134.0)

`PipelineTaskRerunConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User provided rerun config to submit a rerun pipelinejob. This includes

- Which task to rerun
- User override input parameters and artifacts.

## Attributes |
|
|---|---|
Name |
Description |
`task_id` |
`int`
Optional. The system generated ID of the task. Retrieved from original run. |
`task_name` |
`str`
Optional. The name of the task. |
`inputs` |
Optional. The runtime input of the task overridden by the user. |
`skip_task` |
`bool`
Optional. Whether to skip this task. Default value is False. |
`skip_downstream_tasks` |
`bool`
Optional. Whether to skip downstream tasks. Default value is False. |

## Classes

### ArtifactList

`ArtifactList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of artifact metadata.

### Inputs

`Inputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime inputs data of the task.

## Methods

### PipelineTaskRerunConfig

`PipelineTaskRerunConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User provided rerun config to submit a rerun pipelinejob. This includes

- Which task to rerun
- User override input parameters and artifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesPager -->

# Class ListFeaturesPager (1.134.0)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse) object, and
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

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesPager

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Annotation -->

# Class Annotation (1.134.0)

`Annotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Annotation. |
`payload_schema_uri` |
`str`
Required. Google Cloud Storage URI points to a YAML file describing payload. The schema is defined as an `OpenAPI 3.0.2 Schema Object |
`payload` |
`google.protobuf.struct_pb2.Value`
Required. The schema of the payload can be found in payload_schema. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Annotation was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Annotation was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`annotation_source` |
Output only. The source of the Annotation. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Annotations. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Annotation(System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Annotation: - "aiplatform.googleapis.com/annotation_set_name": optional, name of the UI's annotation set this Annotation belongs to. If not set, the Annotation is not visible in the UI. - "aiplatform.googleapis.com/payload_schema": output only, its value is the [payload_schema's][google.cloud.aiplatform.v1.Annotation.payload_schema_uri] title. |

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

### Annotation

`Annotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExtensionRequest -->

# Class GetExtensionRequest (1.134.0)

`GetExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.GetExtension.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Extension resource. Format: `projects/{project}/locations/{location}/extensions/{extension}`
|

## Methods

### GetExtensionRequest

`GetExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.GetExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs -->

# Class AutoMlTextClassificationInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataSchemaRequest -->

# Class CreateMetadataSchemaRequest (1.134.0)

`CreateMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataSchema.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the MetadataSchema should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`metadata_schema` |
Required. The MetadataSchema to create. |
`metadata_schema_id` |
`str`
The {metadata_schema} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/metadataSchemas/{metadataschema}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataSchemas in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataSchema.)
|

## Methods

### CreateMetadataSchemaRequest

`CreateMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataSchema.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeaturesPager -->

# Class ListFeaturesPager (1.134.0)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse) object, and
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

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturesPager

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardOperationMetadata -->

# Class CreateTensorboardOperationMetadata (1.134.0)

```
CreateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Tensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Tensorboard. |

## Methods

### CreateTensorboardOperationMetadata

```
CreateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Tensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VideoMetadata -->

# Class VideoMetadata (1.134.0)

`VideoMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describes the input video content.

## Attributes |
|
|---|---|
Name |
Description |
`start_offset` |
`google.protobuf.duration_pb2.Duration`
Optional. The start offset of the video. |
`end_offset` |
`google.protobuf.duration_pb2.Duration`
Optional. The end offset of the video. |

## Methods

### VideoMetadata

`VideoMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describes the input video content.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardOperationMetadata -->

# Class UpdateTensorboardOperationMetadata (1.134.0)

```
UpdateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Tensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Tensorboard. |

## Methods

### UpdateTensorboardOperationMetadata

```
UpdateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Tensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig.Scaled -->

# Class Scaled (1.134.0)

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

## Methods

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs -->

# Class AutoMlVideoClassificationInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteScheduleRequest -->

# Class DeleteScheduleRequest (1.134.0)

`DeleteScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.DeleteSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be deleted. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### DeleteScheduleRequest

`DeleteScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.DeleteSchedule.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsResponse -->

# Class BatchDeletePipelineJobsResponse (1.134.0)

```
BatchDeletePipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchDeletePipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
PipelineJobs deleted. |

## Methods

### BatchDeletePipelineJobsResponse

```
BatchDeletePipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchDeletePipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs -->

# Class AutoMlVideoObjectTrackingInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationConfig -->

# Class EvaluationConfig (1.134.0)

`EvaluationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation Config for Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`metrics` |
`MutableSequence[`
Required. The metrics used for evaluation. |
`output_config` |
Required. Config for evaluation output. |
`autorater_config` |
Optional. Autorater config for evaluation. |

## Methods

### EvaluationConfig

`EvaluationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation Config for Tuning Job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEndpointRequest -->

# Class DeleteEndpointRequest (1.134.0)

`DeleteEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeleteEndpoint.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Endpoint resource to be deleted. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|

## Methods

### DeleteEndpointRequest

`DeleteEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeleteEndpoint.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictResponse -->

# Class StreamingPredictResponse (1.134.0)

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.

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

### StreamingPredictResponse

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardRequest -->

# Class GetTensorboardRequest (1.134.0)

`GetTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### GetTensorboardRequest

`GetTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboard.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelsAsyncPager -->

# Class ListModelsAsyncPager (1.134.0)

```
ListModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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


A pager for iterating through `list_models`

requests.

This class thinly wraps an initial
[ListModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

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

### ListModelsAsyncPager

```
ListModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsPager -->

# Class ListExecutionsPager (1.134.0)

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse) object, and
provides an `__iter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsPager

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsPager -->

# Class ListSessionsPager (1.134.0)

```
ListSessionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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


A pager for iterating through `list_sessions`

requests.

This class thinly wraps an initial
[ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse) object, and
provides an `__iter__`

method to iterate through its
`sessions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSessions`

requests and continue to iterate
through the `sessions`

field on the
corresponding responses.

All the usual [ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSessionsPager

```
ListSessionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsPager -->

# Class ListDatasetsPager (1.134.0)

```
ListDatasetsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse) object, and
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

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetsPager

```
ListDatasetsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule -->

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
`create_model_monitoring_job_request` |
Request for ModelMonitoringService.CreateModelMonitoringJob. This field is a member of `oneof` _ `request` .
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetOperationMetadata -->

# Class CreateDatasetOperationMetadata (1.134.0)

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDatasetOperationMetadata

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AggregationOutput -->

# Class AggregationOutput (1.134.0)

`AggregationOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for the entire dataset and all metrics.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
The dataset used for evaluation & aggregation. |
`aggregation_results` |
`MutableSequence[`
One AggregationResult per metric. |

## Methods

### AggregationOutput

`AggregationOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for the entire dataset and all metrics.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteCustomJobRequest -->

# Class DeleteCustomJobRequest (1.134.0)

`DeleteCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob resource to be deleted. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### DeleteCustomJobRequest

`DeleteCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteCustomJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModalityTokenCount -->

# Class ModalityTokenCount (1.134.0)

`ModalityTokenCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents token counting info for a single modality.

## Attributes |
|
|---|---|
Name |
Description |
`modality` |
`google.cloud.aiplatform_v1beta1.types.Modality`
The modality associated with this token count. |
`token_count` |
`int`
Number of tokens. |

## Methods

### ModalityTokenCount

`ModalityTokenCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents token counting info for a single modality.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Annotation -->

# Class Annotation (1.134.0)

`Annotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Annotation. |
`payload_schema_uri` |
`str`
Required. Google Cloud Storage URI points to a YAML file describing payload. The schema is defined as an `OpenAPI 3.0.2 Schema Object |
`payload` |
`google.protobuf.struct_pb2.Value`
Required. The schema of the payload can be found in payload_schema. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Annotation was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Annotation was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`annotation_source` |
Output only. The source of the Annotation. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Annotations. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Annotation(System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Annotation: - "aiplatform.googleapis.com/annotation_set_name": optional, name of the UI's annotation set this Annotation belongs to. If not set, the Annotation is not visible in the UI. - "aiplatform.googleapis.com/payload_schema": output only, its value is the [payload_schema's][google.cloud.aiplatform.v1beta1.Annotation.payload_schema_uri] title. |

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

### Annotation

`Annotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to assign specific AnnotationSpec to a particular area of a DataItem or the whole part of the DataItem.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookRuntime -->

# Class NotebookRuntime (1.134.0)

`NotebookRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the NotebookRuntime. |
`runtime_user` |
`str`
Required. The user email of the NotebookRuntime. |
`notebook_runtime_template_ref` |
Output only. The pointer to NotebookRuntimeTemplate this NotebookRuntime is created from. |
`proxy_uri` |
`str`
Output only. The proxy endpoint used to access the NotebookRuntime. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime was most recently updated. |
`health_state` |
Output only. The health state of the NotebookRuntime. |
`display_name` |
`str`
Required. The display name of the NotebookRuntime. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the NotebookRuntime. |
`service_account` |
`str`
Output only. Deprecated: This field is no longer used and the "Vertex AI Notebook Service Account" (service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com) is used for the runtime workload identity. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account for more details. The service account that the NotebookRuntime workload runs as. |
`runtime_state` |
Output only. The runtime (instance) state of the NotebookRuntime. |
`is_upgradable` |
`bool`
Output only. Whether NotebookRuntime is upgradable. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your NotebookRuntime. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one NotebookRuntime (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for NotebookRuntime: - "aiplatform.googleapis.com/notebook_runtime_gce_instance_id": output only, its value is the Compute Engine instance id. - "aiplatform.googleapis.com/colab_enterprise_entry_service": its value is either "bigquery" or "vertex"; if absent, it should be "vertex". This is to describe the entry service, either BigQuery or Vertex. |
`expiration_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime will be expired: 1. System Predefined NotebookRuntime: 24 hours after creation. After expiration, system predifined runtime will be deleted. 2. User created NotebookRuntime: 6 months after last upgrade. After expiration, user created runtime will be stopped and allowed for upgrade. |
`version` |
`str`
Output only. The VM os image version of NotebookRuntime. |
`notebook_runtime_type` |
Output only. The type of the notebook runtime. |
`machine_spec` |
Output only. The specification of a single machine used by the notebook runtime. |
`data_persistent_disk_spec` |
Output only. The specification of [persistent disk][https://cloud.google.com/compute/docs/disks/persistent-disks] attached to the notebook runtime as data disk storage. |
`network_spec` |
Output only. Network spec of the notebook runtime. |
`idle_shutdown_config` |
Output only. The idle shutdown configuration of the notebook runtime. |
`euc_config` |
Output only. EUC configuration of the notebook runtime. |
`shielded_vm_config` |
Output only. Runtime Shielded VM spec. |
`network_tags` |
`MutableSequence[str]`
Optional. The Compute Engine tags to add to runtime (see `Tagging instances |
`software_config` |
Output only. Software config of the notebook runtime. |
`encryption_spec` |
Output only. Customer-managed encryption key spec for the notebook runtime. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### HealthState

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

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

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Methods

### NotebookRuntime

`NotebookRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.InputDataConfig -->

# Class InputDataConfig (1.134.0)

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

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
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`filter_split` |
Split based on the provided filters for each set. This field is a member of `oneof` _ `split` .
|
`predefined_split` |
Supported only for tabular Datasets. Split based on a predefined key. This field is a member of `oneof` _ `split` .
|
`timestamp_split` |
Supported only for tabular Datasets. Split based on the timestamp of the input data pieces. This field is a member of `oneof` _ `split` .
|
`stratified_split` |
Supported only for tabular Datasets. Split based on the distribution of the specified column. This field is a member of `oneof` _ `split` .
|
`gcs_destination` |
The Cloud Storage location where the training data is to be written to. In the given directory a new directory is created with name: `dataset-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All training input data is written into that
directory.
The Vertex AI environment variables representing Cloud
Storage data URIs are represented in the Cloud Storage
wildcard format to support sharded data. e.g.:
"gs://.../training-\*.jsonl"
- AIP_DATA_FORMAT = "jsonl" for non-tabular data, "csv" for
tabular data
- AIP_TRAINING_DATA_URI =
"gcs_destination/dataset---/training-\*.${AIP_DATA_FORMAT}"
- AIP_VALIDATION_DATA_URI =
"gcs_destination/dataset---/validation-\*.${AIP_DATA_FORMAT}"
- AIP_TEST_DATA_URI =
"gcs_destination/dataset---/test-\*.${AIP_DATA_FORMAT}".
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
Only applicable to custom training with tabular Dataset with BigQuery source. The BigQuery project location where the training data is to be written to. In the given project a new dataset is created with name `dataset_`
where timestamp is in YYYY_MM_DDThh_mm_ss_sssZ format. All
training input data is written into that dataset. In the
dataset three tables are created, `training` ,
`validation` and `test` .
- AIP_DATA_FORMAT = "bigquery".
- AIP_TRAINING_DATA_URI =
"bigquery_destination.dataset\_\ **\ .training"
- AIP_VALIDATION_DATA_URI =
"bigquery_destination.dataset\_\ **\ .validation"
- AIP_TEST_DATA_URI =
"bigquery_destination.dataset\_\ **\ .test".
This field is a member of `oneof` _ `destination` .
|
`dataset_id` |
`str`
Required. The ID of the Dataset in the same Project and Location which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1.TrainingPipeline.training_task_definition]. For tabular Datasets, all their data is exported to training, to pick and choose from. |
`annotations_filter` |
`str`
Applicable only to Datasets that have DataItems and Annotations. A filter on Annotations of the Dataset. Only Annotations that both match this filter and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on (for the auto-assigned that role is decided by Vertex AI). A filter with same syntax as the one used in ListAnnotations may be used, but note here it filters across all Annotations of the Dataset, and not just within a single DataItem. |
`annotation_schema_uri` |
`str`
Applicable only to custom training with Datasets that have DataItems and Annotations. Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`saved_query_id` |
`str`
Only applicable to Datasets that have SavedQueries. The ID of a SavedQuery (annotation set) under the Dataset specified by dataset_id used for filtering Annotations for training. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`persist_ml_use_assignment` |
`bool`
Whether to persist the ML use assignment to data item system labels. |

## Methods

### InputDataConfig

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest -->

# Class GetPipelineJobRequest (1.134.0)

`GetPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetPipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### GetPipelineJobRequest

`GetPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetPipelineJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec.NotificationChannelConfig -->

# Class NotificationChannelConfig (1.134.0)

`NotificationChannelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google Cloud Notification Channel config.

## Attribute |
|
|---|---|
Name |
Description |
`notification_channel` |
`str`
Resource names of the NotificationChannels. Must be of the format `projects/`
|

## Methods

### NotificationChannelConfig

`NotificationChannelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google Cloud Notification Channel config.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataSchemaRequest -->

# Class CreateMetadataSchemaRequest (1.134.0)

`CreateMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataSchema.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the MetadataSchema should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`metadata_schema` |
Required. The MetadataSchema to create. |
`metadata_schema_id` |
`str`
The {metadata_schema} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/metadataSchemas/{metadataschema}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataSchemas in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataSchema.)
|

## Methods

### CreateMetadataSchemaRequest

`CreateMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataSchema.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TaskDescriptionStrategy -->

# Class TaskDescriptionStrategy (1.134.0)

`TaskDescriptionStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a generation strategy based on a high-level task description.

## Attribute |
|
|---|---|
Name |
Description |
`task_description` |
`str`
Required. A high-level description of the synthetic data to be generated. |

## Methods

### TaskDescriptionStrategy

`TaskDescriptionStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a generation strategy based on a high-level task description.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataOperationMetadata -->

# Class AssembleDataOperationMetadata (1.134.0)

```
AssembleDataOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.AssembleData.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### AssembleDataOperationMetadata

```
AssembleDataOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.AssembleData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service -->

# Package llm_utility_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.llm_utility_service`

package.

## Classes

[LlmUtilityServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient)

Service for LLM related utility functions.

[LlmUtilityServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient)

Service for LLM related utility functions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJobView -->

# Class NotebookExecutionJobView (1.134.0)

`NotebookExecutionJobView(value)`


Views for Get/List NotebookExecutionJob

## Enums |
|
|---|---|
Name |
Description |
`NOTEBOOK_EXECUTION_JOB_VIEW_UNSPECIFIED` |
When unspecified, the API defaults to the BASIC view. |
`NOTEBOOK_EXECUTION_JOB_VIEW_BASIC` |
Includes all fields except for direct notebook inputs. |
`NOTEBOOK_EXECUTION_JOB_VIEW_FULL` |
Includes all fields. |

## Methods

### NotebookExecutionJobView

`NotebookExecutionJobView(value)`


Views for Get/List NotebookExecutionJob

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntime -->

# Class NotebookRuntime (1.134.0)

`NotebookRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the NotebookRuntime. |
`runtime_user` |
`str`
Required. The user email of the NotebookRuntime. |
`notebook_runtime_template_ref` |
Output only. The pointer to NotebookRuntimeTemplate this NotebookRuntime is created from. |
`proxy_uri` |
`str`
Output only. The proxy endpoint used to access the NotebookRuntime. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime was most recently updated. |
`health_state` |
Output only. The health state of the NotebookRuntime. |
`display_name` |
`str`
Required. The display name of the NotebookRuntime. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the NotebookRuntime. |
`service_account` |
`str`
Output only. Deprecated: This field is no longer used and the "Vertex AI Notebook Service Account" (service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com) is used for the runtime workload identity. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account for more details. The service account that the NotebookRuntime workload runs as. |
`runtime_state` |
Output only. The runtime (instance) state of the NotebookRuntime. |
`is_upgradable` |
`bool`
Output only. Whether NotebookRuntime is upgradable. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your NotebookRuntime. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one NotebookRuntime (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for NotebookRuntime: - "aiplatform.googleapis.com/notebook_runtime_gce_instance_id": output only, its value is the Compute Engine instance id. - "aiplatform.googleapis.com/colab_enterprise_entry_service": its value is either "bigquery" or "vertex"; if absent, it should be "vertex". This is to describe the entry service, either BigQuery or Vertex. |
`expiration_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this NotebookRuntime will be expired: 1. System Predefined NotebookRuntime: 24 hours after creation. After expiration, system predifined runtime will be deleted. 2. User created NotebookRuntime: 6 months after last upgrade. After expiration, user created runtime will be stopped and allowed for upgrade. |
`version` |
`str`
Output only. The VM os image version of NotebookRuntime. |
`notebook_runtime_type` |
Output only. The type of the notebook runtime. |
`machine_spec` |
Output only. The specification of a single machine used by the notebook runtime. |
`data_persistent_disk_spec` |
Output only. The specification of [persistent disk][https://cloud.google.com/compute/docs/disks/persistent-disks] attached to the notebook runtime as data disk storage. |
`network_spec` |
Output only. Network spec of the notebook runtime. |
`idle_shutdown_config` |
Output only. The idle shutdown configuration of the notebook runtime. |
`euc_config` |
Output only. EUC configuration of the notebook runtime. |
`shielded_vm_config` |
Output only. Runtime Shielded VM spec. |
`network_tags` |
`MutableSequence[str]`
Optional. The Compute Engine tags to add to runtime (see `Tagging instances |
`software_config` |
Output only. Software config of the notebook runtime. |
`encryption_spec` |
Output only. Customer-managed encryption key spec for the notebook runtime. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### HealthState

`HealthState(value)`


The substate of the NotebookRuntime to display health information.

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

### RuntimeState

`RuntimeState(value)`


The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

## Methods

### NotebookRuntime

`NotebookRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager -->

# Class ListTrialsAsyncPager (1.134.0)

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__aiter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__aiter__`

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

### ListTrialsAsyncPager

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringScheduleConfig -->

# Class ModelDeploymentMonitoringScheduleConfig (1.134.0)

```
ModelDeploymentMonitoringScheduleConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for scheduling monitoring job.

## Attributes |
|
|---|---|
Name |
Description |
`monitor_interval` |
`google.protobuf.duration_pb2.Duration`
Required. The model monitoring job scheduling interval. It will be rounded up to next full hour. This defines how often the monitoring jobs are triggered. |
`monitor_window` |
`google.protobuf.duration_pb2.Duration`
The time window of the prediction data being included in each prediction dataset. This window specifies how long the data should be collected from historical model results for each run. If not set, ModelDeploymentMonitoringScheduleConfig.monitor_interval will be used. e.g. If currently the cutoff time is 2022-01-08 14:30:00 and the monitor_window is set to be 3600, then data from 2022-01-08 13:30:00 to 2022-01-08 14:30:00 will be retrieved and aggregated to calculate the monitoring statistics. |

## Methods

### ModelDeploymentMonitoringScheduleConfig

```
ModelDeploymentMonitoringScheduleConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for scheduling monitoring job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsResponse -->

# Class BatchCancelPipelineJobsResponse (1.134.0)

```
BatchCancelPipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchCancelPipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
PipelineJobs cancelled. |

## Methods

### BatchCancelPipelineJobsResponse

```
BatchCancelPipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.Algorithm -->

# Class Algorithm (1.134.0)

`Algorithm(value)`


The available search algorithms for the Study.

## Enums |
|
|---|---|
Name |
Description |
`ALGORITHM_UNSPECIFIED` |
The default algorithm used by Vertex AI for `hyperparameter tuning |
`GRID_SEARCH` |
Simple grid search within the feasible space. To use grid search, all parameters must be `INTEGER`, `CATEGORICAL`, or `DISCRETE`. |
`RANDOM_SEARCH` |
Simple random search within the feasible space. |

## Methods

### Algorithm

`Algorithm(value)`


The available search algorithms for the Study.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsAsyncPager -->

# Class ListNasJobsAsyncPager (1.134.0)

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

## Methods

### ListNasJobsAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListContextsPager -->

# Class ListContextsPager (1.134.0)

```
ListContextsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
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


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse) object, and
provides an `__iter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListContextsPager

```
ListContextsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.InputDataConfig -->

# Class InputDataConfig (1.134.0)

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

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
`fraction_split` |
Split based on fractions defining the size of each set. This field is a member of `oneof` _ `split` .
|
`filter_split` |
Split based on the provided filters for each set. This field is a member of `oneof` _ `split` .
|
`predefined_split` |
Supported only for tabular Datasets. Split based on a predefined key. This field is a member of `oneof` _ `split` .
|
`timestamp_split` |
Supported only for tabular Datasets. Split based on the timestamp of the input data pieces. This field is a member of `oneof` _ `split` .
|
`stratified_split` |
Supported only for tabular Datasets. Split based on the distribution of the specified column. This field is a member of `oneof` _ `split` .
|
`gcs_destination` |
The Cloud Storage location where the training data is to be written to. In the given directory a new directory is created with name: `dataset-`
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format. All training input data is written into that
directory.
The Vertex AI environment variables representing Cloud
Storage data URIs are represented in the Cloud Storage
wildcard format to support sharded data. e.g.:
"gs://.../training-\*.jsonl"
- AIP_DATA_FORMAT = "jsonl" for non-tabular data, "csv" for
tabular data
- AIP_TRAINING_DATA_URI =
"gcs_destination/dataset---/training-\*.${AIP_DATA_FORMAT}"
- AIP_VALIDATION_DATA_URI =
"gcs_destination/dataset---/validation-\*.${AIP_DATA_FORMAT}"
- AIP_TEST_DATA_URI =
"gcs_destination/dataset---/test-\*.${AIP_DATA_FORMAT}".
This field is a member of `oneof` _ `destination` .
|
`bigquery_destination` |
Only applicable to custom training with tabular Dataset with BigQuery source. The BigQuery project location where the training data is to be written to. In the given project a new dataset is created with name `dataset_`
where timestamp is in YYYY_MM_DDThh_mm_ss_sssZ format. All
training input data is written into that dataset. In the
dataset three tables are created, `training` ,
`validation` and `test` .
- AIP_DATA_FORMAT = "bigquery".
- AIP_TRAINING_DATA_URI =
"bigquery_destination.dataset\_\ **\ .training"
- AIP_VALIDATION_DATA_URI =
"bigquery_destination.dataset\_\ **\ .validation"
- AIP_TEST_DATA_URI =
"bigquery_destination.dataset\_\ **\ .test".
This field is a member of `oneof` _ `destination` .
|
`dataset_id` |
`str`
Required. The ID of the Dataset in the same Project and Location which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For tabular Datasets, all their data is exported to training, to pick and choose from. |
`annotations_filter` |
`str`
Applicable only to Datasets that have DataItems and Annotations. A filter on Annotations of the Dataset. Only Annotations that both match this filter and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on (for the auto-assigned that role is decided by Vertex AI). A filter with same syntax as the one used in ListAnnotations may be used, but note here it filters across all Annotations of the Dataset, and not just within a single DataItem. |
`annotation_schema_uri` |
`str`
Applicable only to custom training with Datasets that have DataItems and Annotations. Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`saved_query_id` |
`str`
Only applicable to Datasets that have SavedQueries. The ID of a SavedQuery (annotation set) under the Dataset specified by dataset_id used for filtering Annotations for training. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`persist_ml_use_assignment` |
`bool`
Whether to persist the ML use assignment to data item system labels. |

## Methods

### InputDataConfig

`InputDataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies Vertex AI owned input data to be used for training, and possibly evaluating, the Model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob -->

# Class PipelineJob (1.134.0)

`PipelineJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a machine learning PipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the PipelineJob. |
`display_name` |
`str`
The display name of the Pipeline. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline creation time. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline start time. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline end time. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this PipelineJob was most recently updated. |
`pipeline_spec` |
`google.protobuf.struct_pb2.Struct`
The spec of the pipeline. |
`state` |
Output only. The detailed state of the job. |
`job_detail` |
Output only. The details of pipeline run. Not available in the list view. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during pipeline execution. Only populated when the pipeline's state is FAILED or CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize PipelineJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. Note there is some reserved label key for Vertex AI Pipelines. - `vertex-ai-pipelines-run-billing-id` , user set value
will get overrided.
|
`runtime_config` |
Runtime config of the pipeline. |
`encryption_spec` |
Customer-managed encryption key spec for a pipelineJob. If set, this PipelineJob and all of its sub-resources will be secured by this key. |
`service_account` |
`str`
The service account that the pipeline workload runs as. If not specified, the Compute Engine default service account in the project will be used. See https://cloud.google.com/compute/docs/access/service-accounts#default_service_account Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`network` |
`str`
The full name of the Compute Engine `network ` __
to which the Pipeline Job's workload should be peered. For
example, `projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
Private services access must already be configured for the
network. Pipeline job will apply the network configuration
to the Google Cloud resources being launched, if applied,
such as Vertex AI Training or Dataflow job. If left
unspecified, the workload is not peered with any network.
|
`reserved_ip_ranges` |
`MutableSequence[str]`
A list of names for the reserved ip ranges under the VPC network that can be used for this Pipeline Job's workload. If set, we will deploy the Pipeline Job's workload within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for PipelineJob. |
`template_uri` |
`str`
A template uri from where the PipelineJob.pipeline_spec, if empty, will be downloaded. Currently, only uri from Vertex Template Registry & Gallery is supported. Reference to https://cloud.google.com/vertex-ai/docs/pipelines/create-pipeline-template. |
`template_metadata` |
Output only. Pipeline template metadata. Will fill up fields if PipelineJob.template_uri is from supported template registry. |
`schedule_name` |
`str`
Output only. The schedule resource name. Only returned if the Pipeline is created by Schedule API. |
`preflight_validations` |
`bool`
Optional. Whether to do component level validations before job creation. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`original_pipeline_job_id` |
`int`
Optional. The original pipeline job id if this pipeline job is a rerun of a previous pipeline job. |
`pipeline_task_rerun_configs` |
`MutableSequence[`
Optional. The rerun configs for each task in the pipeline job. By default, the rerun will: 1. Use the same input artifacts as the original run. 2. Use the same input parameters as the original run. 3. Skip all the tasks that are already succeeded in the original run. 4. Rerun all the tasks that are not succeeded in the original run. By providing this field, users can override the default behavior and specify the rerun config for each task. |

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

### RuntimeConfig

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime config of a PipelineJob.

## Methods

### PipelineJob

`PipelineJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a machine learning PipelineJob.
