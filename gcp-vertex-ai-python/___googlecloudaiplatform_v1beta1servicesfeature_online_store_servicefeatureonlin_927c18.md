---
merged_at: 2026-01-25T21:47:44.359270
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_online_store_servicefeatureonline_b1cec5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_online_store_servicefeatureonlines_0d61c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_servicefeatureonlinestoreserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient -->

# Class FeatureOnlineStoreServiceAsyncClient (1.134.0)

```
FeatureOnlineStoreServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### FeatureOnlineStoreServiceAsyncClient

```
FeatureOnlineStoreServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature online store service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureOnlineStoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### feature_view_direct_write

```
feature_view_direct_write(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDirectWriteRequest
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
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDirectWriteResponse
]
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
async def sample_feature_view_direct_write():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
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
stream = await client.[feature_view_direct_write](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_feature_view_direct_write)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for FeatureOnlineStoreService.FeatureViewDirectWrite. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_fetch_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest.html)(
id="id_value",
feature_view="feature_view_value",
)
# Make the request
response = await client.[fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_fetch_feature_values)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned. |
`feature_view` |
Required. FeatureView resource format |
`data_key` |
Optional. The request key to fetch feature values for. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
`FeatureOnlineStoreServiceAsyncClient` |
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
`FeatureOnlineStoreServiceAsyncClient` |
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
`FeatureOnlineStoreServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_generate_fetch_access_token():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GenerateFetchAccessTokenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest.html)(
)
# Make the request
response = await client.[generate_fetch_access_token](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_generate_fetch_access_token)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][]. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_search_nearest_entities():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[NearestNeighborQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.html)()
query.entity_id = "entity_id_value"
request = aiplatform_v1beta1.[SearchNearestEntitiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest.html)(
feature_view="feature_view_value",
query=query,
)
# Make the request
response = await client.[search_nearest_entities](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_search_nearest_entities)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for FeatureOnlineStoreService.SearchNearestEntities. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### streaming_fetch_feature_values

```
streaming_fetch_feature_values(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.StreamingFetchFeatureValuesRequest
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
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.StreamingFetchFeatureValuesResponse
]
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
async def sample_streaming_fetch_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
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
stream = await client.[streaming_fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_streaming_fetch_feature_values)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for FeatureOnlineStoreService.StreamingFetchFeatureValues. For the entities requested, all features under the requested feature view will be returned. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstudyspecparameterspec__googlecloudaiplatfo_00a9b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstudyspecparameterspec__googlecloudaiplatfor_b31a72.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudyspecparameterspec__googlecloudaiplatform_e97afa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecparameterspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec -->

# Class ParameterSpec (1.134.0)

`ParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single parameter to optimize.

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
`double_value_spec` |
The value spec for a 'DOUBLE' parameter. This field is a member of `oneof` _ `parameter_value_spec` .
|
`integer_value_spec` |
The value spec for an 'INTEGER' parameter. This field is a member of `oneof` _ `parameter_value_spec` .
|
`categorical_value_spec` |
The value spec for a 'CATEGORICAL' parameter. This field is a member of `oneof` _ `parameter_value_spec` .
|
`discrete_value_spec` |
The value spec for a 'DISCRETE' parameter. This field is a member of `oneof` _ `parameter_value_spec` .
|
`parameter_id` |
`str`
Required. The ID of the parameter. Must not contain whitespaces and must be unique amongst all ParameterSpecs. |
`scale_type` |
How the parameter should be scaled. Leave unset for `CATEGORICAL` parameters.
|
`conditional_parameter_specs` |
`MutableSequence[`
A conditional parameter node is active if the parameter's value matches the conditional node's parent_value_condition. If two items in conditional_parameter_specs have the same name, they must have disjoint parent_value_condition. |

## Classes

### CategoricalValueSpec

`CategoricalValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `CATEGORICAL`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ConditionalParameterSpec

`ConditionalParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a parameter spec with condition from its parent parameter.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DiscreteValueSpec

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DoubleValueSpec

`DoubleValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DOUBLE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### IntegerValueSpec

`IntegerValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `INTEGER`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ScaleType

`ScaleType(value)`


The type of scaling that should be applied to this parameter.

## Methods

### ParameterSpec

`ParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single parameter to optimize.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesextension__googlecloudaiplatform_v1beta1types_0cbccf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesextension.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Extension -->

# Class Extension (1.134.0)

`Extension(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Extensions are tools for large language models to access external data, run computations, etc.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the Extension. |
`display_name` |
`str`
Required. The display name of the Extension. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the Extension. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Extension was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Extension was most recently updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`manifest` |
Required. Manifest of the Extension. |
`extension_operations` |
`MutableSequence[`
Output only. Supported operations. |
`runtime_config` |
Optional. Runtime config controlling the runtime behavior of this Extension. |
`tool_use_examples` |
`MutableSequence[`
Optional. Examples to illustrate the usage of the extension as a tool. |
`private_service_connect_config` |
Optional. The PrivateServiceConnect config for the extension. If specified, the service endpoints associated with the Extension should be registered with private network access in the provided Service Directory (https://cloud.google.com/service-directory/docs/configuring-private-network-access). If the service contains more than one endpoint with a network, the service will arbitrarilty choose one of the endpoints to use for extension execution. |

## Methods

### Extension

`Extension(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Extensions are tools for large language models to access external data, run computations, etc.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatereasoningenginerequest_googlecloudaipla_602d01.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatereasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateReasoningEngineRequest -->

# Class CreateReasoningEngineRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service -->

# Package tensorboard_service (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmutatedeployedindexoperationmetadata_google_f9ade0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmutatedeployedindexoperationmetadata_googlec_dbc82b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmutatedeployedindexoperationmetadata_googlecl_a59e37.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmutatedeployedindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexOperationMetadata -->

# Class MutateDeployedIndexOperationMetadata (1.134.0)

```
MutateDeployedIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.MutateDeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployed_index_id` |
`str`
The unique index id specified by user |

## Methods

### MutateDeployedIndexOperationMetadata

```
MutateDeployedIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.MutateDeployedIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportmodelevaluationrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportModelEvaluationRequest -->

# Class ImportModelEvaluationRequest (1.134.0)

```
ImportModelEvaluationRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ImportModelEvaluation

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent model resource. Format: `projects/{project}/locations/{location}/models/{model}`
|
`model_evaluation` |
Required. Model evaluation resource to be imported. |

## Methods

### ImportModelEvaluationRequest

```
ImportModelEvaluationRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ImportModelEvaluation


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureonlinestorebigtablebigtablemetadata_googlec_fe5045.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestorebigtablebigtablemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Bigtable.BigtableMetadata -->

# Class BigtableMetadata (1.134.0)

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

## Attributes |
|
|---|---|
Name |
Description |
`tenant_project_id` |
`str`
Tenant project ID. |
`instance_id` |
`str`
The Cloud Bigtable instance id. |
`table_id` |
`str`
The Cloud Bigtable table id. |

## Methods

### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchimportmodelevaluationslicesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesResponse -->

# Class BatchImportModelEvaluationSlicesResponse (1.134.0)

```
BatchImportModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportModelEvaluationSlices

## Attribute |
|
|---|---|
Name |
Description |
`imported_model_evaluation_slices` |
`MutableSequence[str]`
Output only. List of imported ModelEvaluationSlice.name. |

## Methods

### BatchImportModelEvaluationSlicesResponse

```
BatchImportModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportModelEvaluationSlices


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistexecutionsresponse_googlecloudaiplatform_5bd15e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistexecutionsresponse_googlecloudaiplatform__b23555.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistexecutionsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse -->

# Class ListExecutionsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetmodelmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitoringJobRequest -->

# Class GetModelMonitoringJobRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdiskspec_googlecloudaiplatform_v1beta1typesge_152044.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdiskspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DiskSpec -->

# Class DiskSpec (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetfeaturemonitorjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest -->

# Class GetFeatureMonitorJobRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstudyspecmeasurementselectiontype__googlecl_49c9b3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstudyspecmeasurementselectiontype__googleclo_8202bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudyspecmeasurementselectiontype__googleclou_693d03.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecmeasurementselectiontype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.MeasurementSelectionType -->

# Class MeasurementSelectionType (1.134.0)

`MeasurementSelectionType(value)`


This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose LAST_MEASUREMENT. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose BEST_MEASUREMENT. B) Are your measurements significantly noisy and/or irreproducible? If so, BEST_MEASUREMENT will tend to be over-optimistic, and it may be better to choose LAST_MEASUREMENT. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen.

## Enums |
|
|---|---|
Name |
Description |
`MEASUREMENT_SELECTION_TYPE_UNSPECIFIED` |
Will be treated as LAST_MEASUREMENT. |
`LAST_MEASUREMENT` |
Use the last measurement reported. |
`BEST_MEASUREMENT` |
Use the best measurement reported. |

## Methods

### MeasurementSelectionType

`MeasurementSelectionType(value)`


This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose LAST_MEASUREMENT. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose BEST_MEASUREMENT. B) Are your measurements significantly noisy and/or irreproducible? If so, BEST_MEASUREMENT will tend to be over-optimistic, and it may be better to choose LAST_MEASUREMENT. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslisttensorboardsresponse_googlecloudaiplatform_v1b_61c31b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttensorboardsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse -->

# Class ListTensorboardsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetnotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest -->

# Class GetNotebookRuntimeTemplateRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdatereasoningenginerequest_googlecloudaiplatfor_7751db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatereasoningenginerequest_googlecloudaiplatform_aa03a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatereasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateReasoningEngineRequest -->

# Class UpdateReasoningEngineRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesshieldedvmconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ShieldedVmConfig -->

# Class ShieldedVmConfig (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessamplingstrategy_googlecloudaiplatform_v1beta_52f590.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessamplingstrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SamplingStrategy -->

# Class SamplingStrategy (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletedeploymentresourcepoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDeploymentResourcePoolRequest -->

# Class DeleteDeploymentResourcePoolRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistpublishermodelsresponse_googlecloudaipl_25e735.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistpublishermodelsresponse_googlecloudaipla_202262.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistpublishermodelsresponse_googlecloudaiplat_df4fa4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistpublishermodelsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse -->

# Class ListPublisherModelsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateragengineconfigrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest -->

# Class UpdateRagEngineConfigRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletemodelmonitorrequest_googlecloudaiplatfo_3b8c03.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletemodelmonitorrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitorRequest -->

# Class DeleteModelMonitorRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardblob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardBlob -->

# Class TensorboardBlob (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesimportragfilesresponse__googlecloudaiplatform_v1ty_926161.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportragfilesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportRagFilesResponse -->

# Class ImportRagFilesResponse (1.134.0)

`ImportRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ImportRagFiles.

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
`partial_failures_gcs_path` |
`str`
The Google Cloud Storage path into which the partial failures were written. This field is a member of `oneof` _ `partial_failure_sink` .
|
`partial_failures_bigquery_table` |
`str`
The BigQuery table into which the partial failures were written. This field is a member of `oneof` _ `partial_failure_sink` .
|
`imported_rag_files_count` |
`int`
The number of RagFiles that had been imported into the RagCorpus. |
`failed_rag_files_count` |
`int`
The number of RagFiles that had failed while importing into the RagCorpus. |
`skipped_rag_files_count` |
`int`
The number of RagFiles that was skipped while importing into the RagCorpus. |

## Methods

### ImportRagFilesResponse

`ImportRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ImportRagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdateendpointlongrunningrequest_googlecloudaiplat_c172cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateendpointlongrunningrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesvertexaisearchconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexAiSearchConfig -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformentitytype_____googlecloudaiplatform_v1beta1typesassessda_2f3ce2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformentitytype_____googlecloudaiplatform_v1beta1typesassessdat_103a86.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformentitytype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType -->

# Class EntityType (1.134.0)

```
EntityType(
entity_type_name: str,
featurestore_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Public managed EntityType resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### featurestore_name

Full qualified resource name of the managed featurestore in which this EntityType is.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### preview

Exposes features available in preview for this class.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### EntityType

```
EntityType(
entity_type_name: str,
featurestore_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed entityType given an entityType resource name or an entity_type ID.

Example Usage:

```
my_entity_type = aiplatform.EntityType(
entity_type_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id'
)
or
my_entity_type = aiplatform.EntityType(
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`entity_type_name` |
`str`
Required. A fully-qualified entityType resource name or an entity_type ID. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id/entityTypes/my_entity_type_id" or "my_entity_type_id" when project and location are initialized or passed, with featurestore_id passed. |
`featurestore_id` |
`str`
Optional. Featurestore ID of an existing featurestore to retrieve entityType from, when entity_type_name is passed as entity_type ID. |
`project` |
`str`
Optional. Project to retrieve entityType from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve entityType from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this EntityType. Overrides credentials set in aiplatform.init. |

### batch_create_features

```
batch_create_features(
feature_configs: typing.Dict[
str, typing.Dict[str, typing.Union[bool, int, typing.Dict[str, str], str]]
],
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
) -> google.cloud.aiplatform.featurestore._entity_type._EntityType
```


Batch creates Feature resources in this EntityType.

Example Usage:

```
my_entity_type = aiplatform.EntityType(
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
my_entity_type.batch_create_features(
feature_configs={
"my_feature_id1": {
"value_type": "INT64",
},
"my_feature_id2": {
"value_type": "BOOL",
},
"my_feature_id3": {
"value_type": "STRING",
},
}
)
```


### create

```
create(
entity_type_id: str,
featurestore_name: str,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore._entity_type._EntityType
```


Creates an EntityType resource in a Featurestore.

Example Usage:

```
my_entity_type = aiplatform.EntityType.create(
entity_type_id='my_entity_type_id',
featurestore_name='projects/123/locations/us-central1/featurestores/my_featurestore_id'
)
or
my_entity_type = aiplatform.EntityType.create(
entity_type_id='my_entity_type_id',
featurestore_name='my_featurestore_id',
)
```


### create_feature

```
create_feature(
feature_id: str,
value_type: str,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.feature.Feature
```


Creates a Feature resource in this EntityType.

Example Usage:

```
my_entity_type = aiplatform.EntityType(
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
my_feature = my_entity_type.create_feature(
feature_id='my_feature_id',
value_type='INT64',
)
```


Parameters |
|
|---|---|
Name |
Description |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name, which is immutable. This value may be up to 60 characters, and valid characters are |
`value_type` |
`str`
Required. Immutable. Type of Feature value. One of BOOL, BOOL_ARRAY, DOUBLE, DOUBLE_ARRAY, INT64, INT64_ARRAY, STRING, STRING_ARRAY, BYTES. |
`description` |
`str`
Optional. Description of the Feature. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Features. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`sync` |
`bool`
Optional. Whether to execute this creation synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### delete

`delete(sync: bool = True, force: bool = False) -> None`


Deletes this EntityType resource. If force is set to True, all features in this EntityType will be deleted prior to entityType deletion.

WARNING: This deletion is permanent.

Exceptions |
|
|---|---|
Type |
Description |
`FailedPrecondition` |
If features are created in this EntityType and force = False. |

### delete_features

`delete_features(feature_ids: typing.List[str], sync: bool = True) -> None`


Deletes feature resources in this EntityType given their feature IDs. WARNING: This deletion is permanent.

### get_feature

```
get_feature(
feature_id: str,
) -> google.cloud.aiplatform.featurestore.feature.Feature
```


Retrieves an existing managed feature in this EntityType.

Parameter |
|
|---|---|
Name |
Description |
`feature_id` |
`str`
Required. The managed feature resource ID in this EntityType. |

### get_featurestore

```
get_featurestore() -> (
google.cloud.aiplatform.featurestore.featurestore.Featurestore
)
```


Retrieves the managed featurestore in which this EntityType is.

### ingest_from_bq

```
ingest_from_bq(
feature_ids: typing.List[str],
feature_time: typing.Union[str, datetime.datetime],
bq_source_uri: str,
feature_source_fields: typing.Optional[typing.Dict[str, str]] = None,
entity_id_field: typing.Optional[str] = None,
disable_online_serving: typing.Optional[bool] = None,
worker_count: typing.Optional[int] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
ingest_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore._entity_type._EntityType
```


Ingest feature values from BigQuery.

### ingest_from_df

```
ingest_from_df(
feature_ids: typing.List[str],
feature_time: typing.Union[str, datetime.datetime],
df_source: pd.DataFrame,
feature_source_fields: typing.Optional[typing.Dict[str, str]] = None,
entity_id_field: typing.Optional[str] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
ingest_request_timeout: typing.Optional[float] = None,
) -> _EntityType
```


Ingest feature values from DataFrame.

Parameters |
|
|---|---|
Name |
Description |
`feature_ids` |
`List[str]`
Required. IDs of the Feature to import values of. The Features must exist in the target EntityType, or the request will fail. |
`feature_time` |
`Union[str, datetime.datetime]`
Required. The feature_time can be one of: - The source column that holds the Feature timestamp for all Feature values in each entity. Note: The dtype of the source column should be |
`df_source` |
`pd.DataFrame`
Required. Pandas DataFrame containing the source data for ingestion. |
`feature_source_fields` |
`Dict[str, str]`
Optional. User defined dictionary to map ID of the Feature for importing values of to the source column for getting the Feature values from. Specify the features whose ID and source column are not the same. If not provided, the source column need to be the same as the Feature ID. .. rubric:: Example feature_ids = ['my_feature_id_1', 'my_feature_id_2', 'my_feature_id_3'] feature_source_fields = { 'my_feature_id_1': 'my_feature_id_1_source_field', } Note: The source column of 'my_feature_id_1' is 'my_feature_id_1_source_field', The source column of 'my_feature_id_2' is the ID of the feature, same for 'my_feature_id_3'. |
`entity_id_field` |
`str`
Optional. Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`ingest_request_timeout` |
`float`
Optional. The timeout for the ingest request in seconds. |

### ingest_from_gcs

```
ingest_from_gcs(
feature_ids: typing.List[str],
feature_time: typing.Union[str, datetime.datetime],
gcs_source_uris: typing.Union[str, typing.List[str]],
gcs_source_type: str,
feature_source_fields: typing.Optional[typing.Dict[str, str]] = None,
entity_id_field: typing.Optional[str] = None,
disable_online_serving: typing.Optional[bool] = None,
worker_count: typing.Optional[int] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
ingest_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore._entity_type._EntityType
```


Ingest feature values from GCS.

Exceptions |
|
|---|---|
Type |
Description |
`ValueErro` |
if gcs_source_type is not supported.: |

### list

```
list(
featurestore_name: str,
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.featurestore._entity_type._EntityType]
```


Lists existing managed entityType resources in a featurestore, given a featurestore resource name or a featurestore ID.

Example Usage:

```
my_entityTypes = aiplatform.EntityType.list(
featurestore_name='projects/123/locations/us-central1/featurestores/my_featurestore_id'
)
or
my_entityTypes = aiplatform.EntityType.list(
featurestore_name='my_featurestore_id'
)
```


Parameters |
|
|---|---|
Name |
Description |
`featurestore_name` |
`str`
Required. A fully-qualified featurestore resource name or a featurestore ID of an existing featurestore to list entityTypes in. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id" or "my_featurestore_id" when project and location are initialized or passed. |
`filter` |
`str`
Optional. Lists the EntityTypes that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |
`project` |
`str`
Optional. Project to list entityTypes in. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to list entityTypes in. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to list entityTypes. Overrides credentials set in aiplatform.init. |

### list_features

```
list_features(
filter: typing.Optional[str] = None, order_by: typing.Optional[str] = None
) -> typing.List[google.cloud.aiplatform.featurestore.feature.Feature]
```


Lists existing managed feature resources in this EntityType.

Example Usage:

```
my_entity_type = aiplatform.EntityType(
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
my_entityType.list_features()
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. Lists the Features that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |

### read

```
read(
entity_ids: typing.Union[str, typing.List[str]],
feature_ids: typing.Union[str, typing.List[str]] = "*",
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
read_request_timeout: typing.Optional[float] = None,
) -> pd.DataFrame
```


Reads feature values for given feature IDs of given entity IDs in this EntityType.

Parameters |
|
|---|---|
Name |
Description |
`entity_ids` |
`Union[str, List[str]]`
Required. ID for a specific entity, or a list of IDs of entities to read Feature values of. The maximum number of IDs is 100 if a list. |
`feature_ids` |
`Union[str, List[str]]`
Required. ID for a specific feature, or a list of IDs of Features in the EntityType for reading feature values. Default to "*", where value of all features will be read. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`read_request_timeout` |
`float`
Optional. The timeout for the read request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`pd.DataFrame` |
entities' feature values in DataFrame |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Sequence[typing.Tuple[str, str]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore._entity_type._EntityType
```


Updates an existing managed entityType resource.

Example Usage:

```
my_entity_type = aiplatform.EntityType(
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
my_entity_type.update(
description='update my description',
)
```


Parameters |
|
|---|---|
Name |
Description |
`description` |
`str`
Optional. Description of the EntityType. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your EntityTypes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Required. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

### write_feature_values

```
write_feature_values(
instances: typing.Union[
typing.List[
google.cloud.aiplatform_v1.types.featurestore_online_service.WriteFeatureValuesPayload
],
typing.Dict[
str,
typing.Dict[
str,
typing.Union[
int,
str,
float,
bool,
bytes,
typing.List[int],
typing.List[str],
typing.List[float],
typing.List[bool],
],
],
],
pd.DataFrame,
],
feature_time: typing.Union[str, datetime.datetime] = None,
) -> EntityType
```


Streaming ingestion. Write feature values directly to Feature Store.

```
my_entity_type = aiplatform.EntityType(
entity_type_name="my_entity_type_id",
featurestore_id="my_featurestore_id",
)
# writing feature values from a pandas DataFrame without feature timestamp column.
# In this case, current timestamp will be applied to all data.
my_dataframe = pd.DataFrame(
data = [
{"entity_id": "movie_01", "average_rating": 4.9}
],
columns=["entity_id", "average_rating"],
)
my_dataframe = my_df.set_index("entity_id")
my_entity_type.write_feature_values(
instances=my_df
)
# writing feature values from a pandas DataFrame with feature timestamp column
# Example of datetime creation.
feature_time = datetime.datetime(year=2022, month=1, day=1, hour=11, minute=59, second=59)
or
feature_time_str = datetime.datetime.now().isoformat(sep=" ", timespec="milliseconds")
feature_time = datetime.datetime.strptime(feature_time_str, "%Y-%m-%d %H:%M:%S.%f")
my_dataframe = pd.DataFrame(
data = [
{"entity_id": "movie_01", "average_rating": 4.9,
"feature_timestamp": feature_time}
],
columns=["entity_id", "average_rating", "feature_timestamp"],
)
my_dataframe = my_df.set_index("entity_id")
my_entity_type.write_feature_values(
instances=my_df, feature_time="feature_timestamp"
)
# writing feature values with a timestamp. The timestamp will be applied to the entire Dataframe.
my_dataframe = pd.DataFrame(
data = [
{"entity_id": "movie_01", "average_rating": 4.9}
],
columns=["entity_id", "average_rating"],
)
my_dataframe = my_df.set_index("entity_id")
my_entity_type.write_feature_values(
instances=my_df, feature_time=feature_time
)
# writing feature values from a Python dict without timestamp column.
# In this case, current timestamp will be applied to all data.
my_data_dict = {
"movie_02" : {"average_rating": 3.7}
}
my_entity_type.write_feature_values(
instances=my_data_dict
)
# writing feature values from a Python dict with timestamp column
my_data_dict = {
"movie_02" : {"average_rating": 3.7, "feature_timestamp": timestmap}}
}
my_entity_type.write_feature_values(
instances=my_data_dict, feature_time="feature_timestamp"
)
# writing feature values from a Python dict and apply the same Feature_Timestamp
my_data_dict = {
"movie_02" : {"average_rating": 3.7}
}
my_entity_type.write_feature_values(
instances=my_data_dict, feature_time=feature_time
)
# writing feature values from a list of WriteFeatureValuesPayload objects
payloads = [
gca_featurestore_online_service.WriteFeatureValuesPayload(
entity_id="movie_03",
feature_values={
"average_rating": featurestore_online_service.FeatureValue(
string_value="test",
metadata=featurestore_online_service.FeatureValue.Metadata(
generate_time=timestmap
)
}
}
)
]
# when instance is WriteFeatureValuesPayload,
# feature_time param of write_feature_values() is ignored.
my_entity_type.write_feature_values(
instances=payloads
)
# reading back written feature values
my_entity_type.read(
entity_ids=["movie_01", "movie_02", "movie_03"]
)
```


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesassessdatarequestbatchpredictionresourceus_227855.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesassessdatarequestbatchpredictionresourceusa_905312.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesassessdatarequestbatchpredictionresourceusag_471684.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesassessdatarequestbatchpredictionresourceusage_f81bc0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassessdatarequestbatchpredictionresourceusageassessmentconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.BatchPredictionResourceUsageAssessmentConfig -->

# Class BatchPredictionResourceUsageAssessmentConfig (1.134.0)

```
BatchPredictionResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction resource usage assessment.

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. The name of the model used for batch prediction. |

## Methods

### BatchPredictionResourceUsageAssessmentConfig

```
BatchPredictionResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction resource usage assessment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespairwisequestionansweringqualityinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityInput -->

# Class PairwiseQuestionAnsweringQualityInput (1.134.0)

```
PairwiseQuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise question answering quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise question answering quality score metric. |
`instance` |
Required. Pairwise question answering quality instance. |

## Methods

### PairwiseQuestionAnsweringQualityInput

```
PairwiseQuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise question answering quality metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturegroupsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsRequest -->

# Class ListFeatureGroupsRequest (1.134.0)

`ListFeatureGroupsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.ListFeatureGroups.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list FeatureGroups. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the FeatureGroups that match the filter expression. The following fields are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
Examples:
- `create_time > "2020-01-01" OR update_time > "2020-01-01"`
FeatureGroups created or updated after 2020-01-01.
- `labels.env = "prod"` FeatureGroups with label "env" set
to "prod".
|
`page_size` |
`int`
The maximum number of FeatureGroups to return. The service may return fewer than this value. If unspecified, at most 100 FeatureGroups will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous [FeatureGroupAdminService.ListFeatureGroups][] call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to [FeatureGroupAdminService.ListFeatureGroups][] must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields: - `create_time`
- `update_time`
|

## Methods

### ListFeatureGroupsRequest

`ListFeatureGroupsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.ListFeatureGroups.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfact__googlecloudaiplatform_v1typeslistfeatur_d52122.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfact.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Fact -->

# Class Fact (1.134.0)

`Fact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fact used in grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`query` |
`str`
Query that is used to retrieve this fact. This field is a member of `oneof` _ `_query` .
|
`title` |
`str`
If present, it refers to the title of this fact. This field is a member of `oneof` _ `_title` .
|
`uri` |
`str`
If present, this uri links to the source of the fact. This field is a member of `oneof` _ `_uri` .
|
`summary` |
`str`
If present, the summary/snippet of the fact. This field is a member of `oneof` _ `_summary` .
|
`vector_distance` |
`float`
If present, the distance between the query vector and this fact vector. This field is a member of `oneof` _ `_vector_distance` .
|
`score` |
`float`
If present, according to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the fact and its range depends on the metric type. For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the fact. The larger the distance, the less relevant the fact is to the query. The range is [0, 2], while 0 means the most relevant and 2 means the least relevant. This field is a member of `oneof` _ `_score` .
|
`chunk` |
If present, chunk properties. This field is a member of `oneof` _ `_chunk` .
|

## Methods

### Fact

`Fact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The fact used in grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistfeaturestoresresponse_googlecloudaiplatform_v1_e45453.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeaturestoresresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletetensorboardexperimentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardExperimentRequest -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescreatereasoningenginerequest_googlecloudaiplatfo_c1ede6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreatereasoningenginerequest_googlecloudaiplatfor_d8d96f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatereasoningenginerequest_googlecloudaiplatform_99f740.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatereasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateReasoningEngineRequest -->

# Class CreateReasoningEngineRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslineagesubgraph.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LineageSubgraph -->

# Class LineageSubgraph (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetannotationspecrequest_googlecloudaiplatform_v1t_7cd991.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetannotationspecrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetAnnotationSpecRequest -->

# Class GetAnnotationSpecRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborsneighbor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighbors.Neighbor -->

# Class Neighbor (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportragfilesresponse__googlecloudaiplatform_78993e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportragfilesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesResponse -->

# Class ImportRagFilesResponse (1.134.0)

`ImportRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ImportRagFiles.

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
`partial_failures_gcs_path` |
`str`
The Google Cloud Storage path into which the partial failures were written. This field is a member of `oneof` _ `partial_failure_sink` .
|
`partial_failures_bigquery_table` |
`str`
The BigQuery table into which the partial failures were written. This field is a member of `oneof` _ `partial_failure_sink` .
|
`imported_rag_files_count` |
`int`
The number of RagFiles that had been imported into the RagCorpus. |
`failed_rag_files_count` |
`int`
The number of RagFiles that had failed while importing into the RagCorpus. |
`skipped_rag_files_count` |
`int`
The number of RagFiles that was skipped while importing into the RagCorpus. |

## Methods

### ImportRagFilesResponse

`ImportRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ImportRagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistoptimaltrialsresponse_googlecloudaiplatfo_e3c3f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistoptimaltrialsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsResponse -->

# Class ListOptimalTrialsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewvectorsearchconfigtreeahconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig.TreeAHConfig -->

# Class TreeAHConfig (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesspecialist_pool_servicespecialistpoolserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient -->

# Class SpecialistPoolServiceAsyncClient (1.134.0)

```
SpecialistPoolServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

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
`SpecialistPoolServiceTransport` |
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

### SpecialistPoolServiceAsyncClient

```
SpecialistPoolServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the specialist pool service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,SpecialistPoolServiceTransport,Callable[..., SpecialistPoolServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the SpecialistPoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_specialist_pool

```
create_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.CreateSpecialistPoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
specialist_pool: typing.Optional[
google.cloud.aiplatform_v1.types.specialist_pool.SpecialistPool
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


Creates a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1.[CreateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateSpecialistPoolRequest.html)(
parent="parent_value",
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[create_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_create_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.CreateSpecialistPool. |
`parent` |
Required. The parent Project name for the new SpecialistPool. The form is |
`specialist_pool` |
Required. The SpecialistPool to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_specialist_pool

```
delete_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.DeleteSpecialistPoolRequest,
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


Deletes a SpecialistPool as well as all Specialists in the pool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_delete_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.DeleteSpecialistPool. |
`name` |
Required. The resource name of the SpecialistPool to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`SpecialistPoolServiceAsyncClient` |
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
`SpecialistPoolServiceAsyncClient` |
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
`SpecialistPoolServiceAsyncClient` |
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

### get_specialist_pool

```
get_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.GetSpecialistPoolRequest,
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
) -> google.cloud.aiplatform_v1.types.specialist_pool.SpecialistPool
```


Gets a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_get_specialist_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for SpecialistPoolService.GetSpecialistPool. |
`name` |
Required. The name of the SpecialistPool resource. The form is |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport
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

### list_specialist_pools

```
list_specialist_pools(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
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
google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager
)
```


Lists SpecialistPools in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_specialist_pools():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSpecialistPoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_specialist_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_list_specialist_pools)(request=request)
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
The request object. Request message for SpecialistPoolService.ListSpecialistPools. |
`parent` |
Required. The name of the SpecialistPool's parent resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for SpecialistPoolService.ListSpecialistPools. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_specialist_pool_path

`parse_specialist_pool_path(path: str) -> typing.Dict[str, str]`


Parses a specialist_pool path into its component segments.

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

### specialist_pool_path

`specialist_pool_path(project: str, location: str, specialist_pool: str) -> str`


Returns a fully-qualified specialist_pool string.

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

### update_specialist_pool

```
update_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.specialist_pool_service.UpdateSpecialistPoolRequest,
dict,
]
] = None,
*,
specialist_pool: typing.Optional[
google.cloud.aiplatform_v1.types.specialist_pool.SpecialistPool
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


Updates a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1.[UpdateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateSpecialistPoolRequest.html)(
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[update_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_update_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.UpdateSpecialistPool. |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesgen_ai_tuning_servicegenaituningserviceas_0068ee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesgen_ai_tuning_servicegenaituningserviceasy_362b04.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_tuning_servicegenaituningserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient -->

# Class GenAiTuningServiceAsyncClient (1.134.0)

```
GenAiTuningServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### GenAiTuningServiceAsyncClient

```
GenAiTuningServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai tuning service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiTuningServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### cancel_tuning_job

```
cancel_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.CancelTuningJobRequest,
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
xref_TuningJob.state
is set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_cancel_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTuningJobRequest.html)(
name="name_value",
)
# Make the request
await client.[cancel_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_cancel_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiTuningService.CancelTuningJob. |
`name` |
Required. The name of the TuningJob to cancel. Format: |
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

### create_tuning_job

```
create_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.CreateTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuning_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tuning_job.TuningJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.tuning_job.TuningJob
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
from google.cloud import aiplatform_v1beta1
async def sample_create_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
tuning_job = aiplatform_v1beta1.[TuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningJob.html)()
tuning_job.base_model = "base_model_value"
tuning_job.supervised_tuning_spec.training_dataset_uri = "training_dataset_uri_value"
request = aiplatform_v1beta1.[CreateTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTuningJobRequest.html)(
parent="parent_value",
tuning_job=tuning_job,
)
# Make the request
response = await client.[create_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_create_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiTuningService.CreateTuningJob. |
`parent` |
Required. The resource name of the Location to create the TuningJob in. Format: |
`tuning_job` |
Required. The TuningJob to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
`GenAiTuningServiceAsyncClient` |
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
`GenAiTuningServiceAsyncClient` |
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
`GenAiTuningServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport
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

### get_tuning_job

```
get_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.GetTuningJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.tuning_job.TuningJob
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
from google.cloud import aiplatform_v1beta1
async def sample_get_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_get_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for GenAiTuningService.GetTuningJob. |
`name` |
Required. The name of the TuningJob resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### list_tuning_jobs

```
list_tuning_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_tuning_jobs():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_list_tuning_jobs)(request=request)
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
The request object. Request message for GenAiTuningService.ListTuningJobs. |
`parent` |
Required. The resource name of the Location to list the TuningJobs from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.RebaseTunedModelRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuned_model_ref: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tuning_job.TunedModelRef
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


Rebase a TunedModel. Creates a LongRunningOperation that takes a legacy Tuned GenAI model Reference and creates a TuningJob based on newly available model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_rebase_tuned_model():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
tuned_model_ref = aiplatform_v1beta1.[TunedModelRef](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelRef.html)()
tuned_model_ref.tuned_model = "tuned_model_value"
request = aiplatform_v1beta1.[RebaseTunedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelRequest.html)(
parent="parent_value",
tuned_model_ref=tuned_model_ref,
)
# Make the request
operation = client.[rebase_tuned_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_rebase_tuned_model)(request=request)
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
The request object. Request message for GenAiTuningService.RebaseTunedModel. |
`parent` |
Required. The resource name of the Location into which to rebase the Model. Format: |
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesmodelgardensource_googlecloudaiplatform_v1beta_5a4684.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesmodelgardensource_googlecloudaiplatform_v1beta1_ad86ac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmodelgardensource_googlecloudaiplatform_v1beta1t_5f70a7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelgardensource_googlecloudaiplatform_v1beta1ty_e0432c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelgardensource_googlecloudaiplatform_v1beta1typ_0ec593.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelgardensource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelGardenSource -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslineagesubgraph.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LineageSubgraph -->

# Class LineageSubgraph (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnotebookexecutionjobcustomenvironmentspec_goo_1a2497.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjobcustomenvironmentspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.CustomEnvironmentSpec -->

# Class CustomEnvironmentSpec (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdirectpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictRequest -->

# Class DirectPredictRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragcontexts_googlecloudaiplatform_v1beta1typ_0a2ba3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragcontexts_googlecloudaiplatform_v1beta1type_d4daae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragcontexts.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagContexts -->

# Class RagContexts (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnearestneighborsneighbor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighbors.Neighbor -->

# Class Neighbor (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatepersistentresourceoperationmetadata_goo_aa2485.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatepersistentresourceoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceOperationMetadata -->

# Class CreatePersistentResourceOperationMetadata (1.134.0)

```
CreatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Create LRO |

## Methods

### CreatePersistentResourceOperationMetadata

```
CreatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create PersistentResource.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltables.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTables -->

# Class AutoMlTables (1.134.0)

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

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

### AutoMlTables

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

### AutoMlTables

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedback_googleclou_fadb2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedback_googlecloud_408fb9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedback_googleclouda_f893c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedback.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse.PromptFeedback -->

# Class PromptFeedback (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratefetchaccesstokenrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest -->

# Class GenerateFetchAccessTokenRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesshieldedvmconfig_googlecloudaiplatform_v1beta_64a25e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesshieldedvmconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ShieldedVmConfig -->

# Class ShieldedVmConfig (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstopnotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest -->

# Class StopNotebookRuntimeRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesrebootpersistentresourcerequest_googlecloudaiplat_559478.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrebootpersistentresourcerequest_googlecloudaiplatf_2f2a23.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrebootpersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest -->

# Class RebootPersistentResourceRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelevaluationsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse -->

# Class ListModelEvaluationsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetfeatureviewsyncrequest_googlecloudaiplatform_v1_260edb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetfeatureviewsyncrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureViewSyncRequest -->

# Class GetFeatureViewSyncRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrubricbasedinstructionfollowinginput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingInput -->

# Class RubricBasedInstructionFollowingInput (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.dataset_service.pagers`

module.

## Classes

[ListAnnotationsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsAsyncPager)

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

[ListAnnotationsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsPager)

```
ListAnnotationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsResponse,
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


A pager for iterating through `list_annotations`

requests.

This class thinly wraps an initial
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse) object, and
provides an `__iter__`

method to iterate through its
`annotations`

field.

If there are more pages, the `__iter__`

method will make additional
`ListAnnotations`

requests and continue to iterate
through the `annotations`

field on the
corresponding responses.

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataItemsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsAsyncPager)

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

[ListDataItemsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsPager)

```
ListDataItemsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse) object, and
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

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetVersionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager)

```
ListDatasetVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse) object, and
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

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetVersionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsPager)

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

[ListDatasetsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsAsyncPager)

```
ListDatasetsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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


A pager for iterating through `list_datasets`

requests.

This class thinly wraps an initial
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse) object, and
provides an `__aiter__`

method to iterate through its
`datasets`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDatasets`

requests and continue to iterate
through the `datasets`

field on the
corresponding responses.

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsPager)

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

[ListSavedQueriesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesAsyncPager)

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

[ListSavedQueriesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesPager)

```
ListSavedQueriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
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


A pager for iterating through `list_saved_queries`

requests.

This class thinly wraps an initial
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse) object, and
provides an `__iter__`

method to iterate through its
`saved_queries`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSavedQueries`

requests and continue to iterate
through the `saved_queries`

field on the
corresponding responses.

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchDataItemsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsAsyncPager)

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

[SearchDataItemsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsPager)

```
SearchDataItemsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesreasoning_engine_servicereasoningengineservicea_046dbb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesreasoning_engine_servicereasoningengineserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient -->

# Class ReasoningEngineServiceAsyncClient (1.134.0)

```
ReasoningEngineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Reasoning Engines.

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
`ReasoningEngineServiceTransport` |
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

### ReasoningEngineServiceAsyncClient

```
ReasoningEngineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineServiceTransport,Callable[..., ReasoningEngineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_reasoning_engine

```
create_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.CreateReasoningEngineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
reasoning_engine: typing.Optional[
google.cloud.aiplatform_v1.types.reasoning_engine.ReasoningEngine
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


Creates a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
reasoning_engine = aiplatform_v1.[ReasoningEngine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngine.html)()
reasoning_engine.display_name = "display_name_value"
request = aiplatform_v1.[CreateReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateReasoningEngineRequest.html)(
parent="parent_value",
reasoning_engine=reasoning_engine,
)
# Make the request
operation = client.[create_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_create_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.CreateReasoningEngine. |
`parent` |
Required. The resource name of the Location to create the ReasoningEngine in. Format: |
`reasoning_engine` |
Required. The ReasoningEngine to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_reasoning_engine

```
delete_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.DeleteReasoningEngineRequest,
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


Deletes a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_delete_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.DeleteReasoningEngine. |
`name` |
Required. The name of the ReasoningEngine resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ReasoningEngineServiceAsyncClient` |
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
`ReasoningEngineServiceAsyncClient` |
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
`ReasoningEngineServiceAsyncClient` |
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

### get_reasoning_engine

```
get_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.GetReasoningEngineRequest,
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
) -> google.cloud.aiplatform_v1.types.reasoning_engine.ReasoningEngine
```


Gets a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_get_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ReasoningEngineService.GetReasoningEngine. |
`name` |
Required. The name of the ReasoningEngine resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport
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

### git_repository_link_path

```
git_repository_link_path(
project: str, location: str, connection: str, git_repository_link: str
) -> str
```


Returns a fully-qualified git_repository_link string.

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

### list_reasoning_engines

```
list_reasoning_engines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
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
google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager
)
```


Lists reasoning engines in a location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_reasoning_engines():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListReasoningEnginesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_reasoning_engines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_list_reasoning_engines)(request=request)
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
The request object. Request message for ReasoningEngineService.ListReasoningEngines. |
`parent` |
Required. The resource name of the Location to list the ReasoningEngines from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ReasoningEngineService.ListReasoningEngines Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### parse_git_repository_link_path

`parse_git_repository_link_path(path: str) -> typing.Dict[str, str]`


Parses a git_repository_link path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### update_reasoning_engine

```
update_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_service.UpdateReasoningEngineRequest,
dict,
]
] = None,
*,
reasoning_engine: typing.Optional[
google.cloud.aiplatform_v1.types.reasoning_engine.ReasoningEngine
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


Updates a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
reasoning_engine = aiplatform_v1.[ReasoningEngine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngine.html)()
reasoning_engine.display_name = "display_name_value"
request = aiplatform_v1.[UpdateReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateReasoningEngineRequest.html)(
reasoning_engine=reasoning_engine,
)
# Make the request
operation = client.[update_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_update_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.UpdateReasoningEngine. |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. This corresponds to the |
`update_mask` |
Optional. Mask specifying which fields to update. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesspecialist_pool_servicespecialistpoolserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient -->

# Class SpecialistPoolServiceAsyncClient (1.134.0)

```
SpecialistPoolServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

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
`SpecialistPoolServiceTransport` |
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

### SpecialistPoolServiceAsyncClient

```
SpecialistPoolServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the specialist pool service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,SpecialistPoolServiceTransport,Callable[..., SpecialistPoolServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the SpecialistPoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_specialist_pool

```
create_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.CreateSpecialistPoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
specialist_pool: typing.Optional[
google.cloud.aiplatform_v1beta1.types.specialist_pool.SpecialistPool
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


Creates a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1beta1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSpecialistPoolRequest.html)(
parent="parent_value",
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[create_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_create_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.CreateSpecialistPool. |
`parent` |
Required. The parent Project name for the new SpecialistPool. The form is |
`specialist_pool` |
Required. The SpecialistPool to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_specialist_pool

```
delete_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.DeleteSpecialistPoolRequest,
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


Deletes a SpecialistPool as well as all Specialists in the pool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_delete_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.DeleteSpecialistPool. |
`name` |
Required. The resource name of the SpecialistPool to delete. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`SpecialistPoolServiceAsyncClient` |
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
`SpecialistPoolServiceAsyncClient` |
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
`SpecialistPoolServiceAsyncClient` |
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

### get_specialist_pool

```
get_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.GetSpecialistPoolRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.specialist_pool.SpecialistPool
```


Gets a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_get_specialist_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for SpecialistPoolService.GetSpecialistPool. |
`name` |
Required. The name of the SpecialistPool resource. The form is |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.transports.base.SpecialistPoolServiceTransport
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

### list_specialist_pools

```
list_specialist_pools(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
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
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager
)
```


Lists SpecialistPools in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_specialist_pools():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSpecialistPoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_specialist_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_list_specialist_pools)(request=request)
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
The request object. Request message for SpecialistPoolService.ListSpecialistPools. |
`parent` |
Required. The name of the SpecialistPool's parent resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for SpecialistPoolService.ListSpecialistPools. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_specialist_pool_path

`parse_specialist_pool_path(path: str) -> typing.Dict[str, str]`


Parses a specialist_pool path into its component segments.

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

### specialist_pool_path

`specialist_pool_path(project: str, location: str, specialist_pool: str) -> str`


Returns a fully-qualified specialist_pool string.

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

### update_specialist_pool

```
update_specialist_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.UpdateSpecialistPoolRequest,
dict,
]
] = None,
*,
specialist_pool: typing.Optional[
google.cloud.aiplatform_v1beta1.types.specialist_pool.SpecialistPool
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


Updates a SpecialistPool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1beta1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSpecialistPoolRequest.html)(
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[update_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceAsyncClient_update_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.UpdateSpecialistPool. |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
