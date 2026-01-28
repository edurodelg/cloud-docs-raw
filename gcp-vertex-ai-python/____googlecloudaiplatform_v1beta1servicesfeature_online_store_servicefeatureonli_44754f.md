---
merged_at: 2026-01-28T15:11:44.762494
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient -->

# Class FeatureOnlineStoreServiceClient (1.135.0)

```
FeatureOnlineStoreServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### FeatureOnlineStoreServiceClient

```
FeatureOnlineStoreServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature online store service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureOnlineStoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### feature_view_direct_write

```
feature_view_direct_write(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDirectWriteRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.FeatureViewDirectWriteResponse
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
def sample_feature_view_direct_write():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
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
stream = client.[feature_view_direct_write](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_feature_view_direct_write)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for FeatureOnlineStoreService.FeatureViewDirectWrite. |
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
`Iterable[` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_fetch_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest.html)(
id="id_value",
feature_view="feature_view_value",
)
# Make the request
response = client.[fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_fetch_feature_values)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned. |
`feature_view` |
`str`
Required. FeatureView resource format |
`data_key` |
Optional. The request key to fetch feature values for. This corresponds to the |
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
`FeatureOnlineStoreServiceClient` |
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
`FeatureOnlineStoreServiceClient` |
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
`FeatureOnlineStoreServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_generate_fetch_access_token():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GenerateFetchAccessTokenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest.html)(
)
# Make the request
response = client.[generate_fetch_access_token](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_generate_fetch_access_token)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][]. |
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
Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][]. |

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
google.api_core.retry.retry_unary.Retry,
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
def sample_search_nearest_entities():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[NearestNeighborQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.html)()
query.entity_id = "entity_id_value"
request = aiplatform_v1beta1.[SearchNearestEntitiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesRequest.html)(
feature_view="feature_view_value",
query=query,
)
# Make the request
response = client.[search_nearest_entities](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_search_nearest_entities)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for FeatureOnlineStoreService.SearchNearestEntities. |
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
Response message for FeatureOnlineStoreService.SearchNearestEntities |

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

### streaming_fetch_feature_values

```
streaming_fetch_feature_values(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.StreamingFetchFeatureValuesRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_service.StreamingFetchFeatureValuesResponse
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
def sample_streaming_fetch_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
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
stream = client.[streaming_fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_streaming_fetch_feature_values)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for FeatureOnlineStoreService.StreamingFetchFeatureValues. For the entities requested, all features under the requested feature view will be returned. |
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
`Iterable[` |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataLabelingJob.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.135.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteFeatureValuesPayload.FeatureValuesEntry -->

# Class FeatureValuesEntry (1.135.0)

`FeatureValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.InputArtifactsEntry -->

# Class InputArtifactsEntry (1.135.0)

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### InputArtifactsEntry

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsRequest -->

# Class ListDatasetVersionsRequest (1.135.0)

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list DatasetVersions from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
Optional. The standard list filter. |
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListDatasetVersionsRequest

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationConfig -->

# Class PSCAutomationConfig (1.135.0)

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project id used to create forwarding rule. |
`network` |
`str`
Required. The full name of the Google Compute Engine `network ` __.
`Format ` __:
`projects/{project}/global/networks/{network}` .
|
`ip_address` |
`str`
Output only. IP address rule created by the PSC service automation. |
`forwarding_rule` |
`str`
Output only. Forwarding rule created by the PSC service automation. |
`state` |
Output only. The state of the PSC service automation. |
`error_message` |
`str`
Output only. Error message if the PSC service automation failed. |

## Methods

### PSCAutomationConfig

`PSCAutomationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PSC config that is used to automatically create PSC endpoints in the user projects.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.135.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction -->

# Class CallToAction (1.135.0)

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### Deploy

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DeployGke

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment

### OpenFineTuningPipelines

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

### OpenNotebooks

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.

### RegionalResourceReferences

`RegionalResourceReferences(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The regional resource name or the URI. Key is region, e.g., us-central1, europe-west2, global, etc..

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ViewRestApi

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

## Methods

### CallToAction

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesRequest -->

# Class EvaluateInstancesRequest (1.135.0)

`EvaluateInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateInstances.

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
`exact_match_input` |
Auto metric instances. Instances and metric spec for exact match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`bleu_input` |
Instances and metric spec for bleu metric. This field is a member of `oneof` _ `metric_inputs` .
|
`rouge_input` |
Instances and metric spec for rouge metric. This field is a member of `oneof` _ `metric_inputs` .
|
`fluency_input` |
LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric. This field is a member of `oneof` _ `metric_inputs` .
|
`coherence_input` |
Input for coherence metric. This field is a member of `oneof` _ `metric_inputs` .
|
`safety_input` |
Input for safety metric. This field is a member of `oneof` _ `metric_inputs` .
|
`groundedness_input` |
Input for groundedness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`fulfillment_input` |
Input for fulfillment metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_quality_input` |
Input for summarization quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_summarization_quality_input` |
Input for pairwise summarization quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_helpfulness_input` |
Input for summarization helpfulness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_verbosity_input` |
Input for summarization verbosity metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_quality_input` |
Input for question answering quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_question_answering_quality_input` |
Input for pairwise question answering quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_relevance_input` |
Input for question answering relevance metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_helpfulness_input` |
Input for question answering helpfulness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_correctness_input` |
Input for question answering correctness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pointwise_metric_input` |
Input for pointwise metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_metric_input` |
Input for pairwise metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_call_valid_input` |
Tool call metric instances. Input for tool call valid metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_name_match_input` |
Input for tool name match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_parameter_key_match_input` |
Input for tool parameter key match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_parameter_kv_match_input` |
Input for tool parameter key value match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`comet_input` |
Translation metrics. Input for Comet metric. This field is a member of `oneof` _ `metric_inputs` .
|
`metricx_input` |
Input for Metricx metric. This field is a member of `oneof` _ `metric_inputs` .
|
`location` |
`str`
Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`
|

## Methods

### EvaluateInstancesRequest

`EvaluateInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateInstances.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content -->

# Class Content (1.135.0)

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

## Attributes |
|
|---|---|
Name |
Description |
`role` |
`str`
Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset. |
`parts` |
`MutableSequence[`
Required. Ordered `Parts` that constitute a single
message. Parts may have different IANA MIME types.
|

## Methods

### Content

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RaySpec.ResourcePoolImagesEntry -->

# Class ResourcePoolImagesEntry (1.135.0)

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolCallValidInstance -->

# Class ToolCallValidInstance (1.135.0)

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

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

### ToolCallValidInstance

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolNameMatchInstance -->

# Class ToolNameMatchInstance (1.135.0)

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

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

### ToolNameMatchInstance

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.135.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseChoice -->

# Class PairwiseChoice (1.135.0)

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

## Enums |
|
|---|---|
Name |
Description |
`PAIRWISE_CHOICE_UNSPECIFIED` |
Unspecified prediction choice. |
`BASELINE` |
Baseline prediction wins |
`CANDIDATE` |
Candidate prediction wins |
`TIE` |
Winner cannot be determined |

## Methods

### PairwiseChoice

`PairwiseChoice(value)`


Pairwise prediction autorater preference.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.PerMonthUsageData -->

# Class PerMonthUsageData (1.135.0)

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

## Attribute |
|
|---|---|
Name |
Description |
`user_usage_data` |
`MutableSequence[`
Usage data for each user in the given month. |

## Methods

### PerMonthUsageData

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.ManualRoutingMode -->

# Class ManualRoutingMode (1.135.0)

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
The model name to use. Only the public LLM models are accepted. e.g. 'gemini-1.5-pro-001'. This field is a member of `oneof` _ `_model_name` .
|

## Methods

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxResult -->

# Class MetricxResult (1.135.0)

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. MetricX score. Range depends on version. This field is a member of `oneof` _ `_score` .
|

## Methods

### MetricxResult

`MetricxResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EntityIdSelector -->

# Class EntityIdSelector (1.135.0)

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`csv_source` |
Source of Csv This field is a member of `oneof` _ `EntityIdsSource` .
|
`entity_id_field` |
`str`
Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity_id. |

## Methods

### EntityIdSelector

`EntityIdSelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selector for entityId. Getting ids from the given source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeArtifact.CustomPropertiesEntry -->

# Class CustomPropertiesEntry (1.135.0)

`CustomPropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### CustomPropertiesEntry

`CustomPropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileConfig -->

# Class UploadRagFileConfig (1.135.0)

`UploadRagFileConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for uploading RagFile.

## Attribute |
|
|---|---|
Name |
Description |
`rag_file_transformation_config` |
Specifies the transformation config for RagFiles. |

## Methods

### UploadRagFileConfig

`UploadRagFileConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for uploading RagFile.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringAlertConfig.EmailAlertConfig -->

# Class EmailAlertConfig (1.135.0)

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Attribute |
|
|---|---|
Name |
Description |
`user_emails` |
`MutableSequence[str]`
The email addresses to send the alert. |

## Methods

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CopyModelRequest -->

# Class CopyModelRequest (1.135.0)

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

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
`model_id` |
`str`
Optional. Copy source_model into a new Model with this ID. The ID will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
This field is a member of `oneof` _ `destination_model` .
|
`parent_model` |
`str`
Optional. Specify this field to copy source_model into this existing Model as a new version. Format: `projects/{project}/locations/{location}/models/{model}`
This field is a member of `oneof` _ `destination_model` .
|
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: `projects/{project}/locations/{location}`
|
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: `projects/{project}/locations/{location}/models/{model}`
|
`encryption_spec` |
Customer-managed encryption key options. If this is set, then the Model copy will be encrypted with the provided encryption key. |

## Methods

### CopyModelRequest

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.InputArtifactsEntry -->

# Class InputArtifactsEntry (1.135.0)

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### InputArtifactsEntry

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.135.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob.RuntimeConfig.ParameterValuesEntry -->

# Class ParameterValuesEntry (1.135.0)

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ParameterValuesEntry

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.AnnotationLabelsEntry -->

# Class AnnotationLabelsEntry (1.135.0)

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertCondition -->

# Class ModelMonitoringAlertCondition (1.135.0)

```
ModelMonitoringAlertCondition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Monitoring alert triggered condition.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`threshold` |
`float`
A condition that compares a stats value against a threshold. Alert will be triggered if value above the threshold. This field is a member of `oneof` _ `condition` .
|

## Methods

### ModelMonitoringAlertCondition

```
ModelMonitoringAlertCondition(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Monitoring alert triggered condition.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest -->

# Class ListDatasetVersionsRequest (1.135.0)

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list DatasetVersions from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
Optional. The standard list filter. |
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListDatasetVersionsRequest

`ListDatasetVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasetVersions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1.services.dataset_service.pagers`

module.

## Classes

[ListAnnotationsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsAsyncPager)

```
ListAnnotationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse) object, and
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

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListAnnotationsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsPager)

```
ListAnnotationsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse) object, and
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

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataItemsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsAsyncPager)

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse) object, and
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

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataItemsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsPager)

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

[ListDatasetVersionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager)

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

[ListDatasetVersionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsPager)

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse) object, and
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

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsAsyncPager)

```
ListDatasetsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsResponse,
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
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse) object, and
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

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDatasetsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsPager)

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

[ListSavedQueriesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesAsyncPager)

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

[ListSavedQueriesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesPager)

```
ListSavedQueriesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesResponse,
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
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse) object, and
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

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchDataItemsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsAsyncPager)

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

[SearchDataItemsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsPager)

```
SearchDataItemsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse) object, and
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

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest -->

# Class CopyModelRequest (1.135.0)

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

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
`model_id` |
`str`
Optional. Copy source_model into a new Model with this ID. The ID will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
This field is a member of `oneof` _ `destination_model` .
|
`parent_model` |
`str`
Optional. Specify this field to copy source_model into this existing Model as a new version. Format: `projects/{project}/locations/{location}/models/{model}`
This field is a member of `oneof` _ `destination_model` .
|
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: `projects/{project}/locations/{location}`
|
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: `projects/{project}/locations/{location}/models/{model}`
|
`encryption_spec` |
Customer-managed encryption key options. If this is set, then the Model copy will be encrypted with the provided encryption key. |

## Methods

### CopyModelRequest

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content -->

# Class Content (1.135.0)

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

## Attributes |
|
|---|---|
Name |
Description |
`role` |
`str`
Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset. |
`parts` |
`MutableSequence[`
Required. Ordered `Parts` that constitute a single
message. Parts may have different IANA MIME types.
|

## Methods

### Content

`Content(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The base structured datatype containing multi-part content of a message.

A `Content`

includes a `role`

field designating the producer of
the `Content`

and a `parts`

field containing multi-part data
that contains the content of the message turn.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RaySpec.ResourcePoolImagesEntry -->

# Class ResourcePoolImagesEntry (1.135.0)

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PartnerModelTuningSpec.HyperParametersEntry -->

# Class HyperParametersEntry (1.135.0)

`HyperParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### HyperParametersEntry

`HyperParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesRequest -->

# Class ReadFeatureValuesRequest (1.135.0)

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the EntityType for the entity being read. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_id` |
`str`
Required. ID for a specific entity. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. |

## Methods

### ReadFeatureValuesRequest

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchInstance -->

# Class ToolNameMatchInstance (1.135.0)

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

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

### ToolNameMatchInstance

`ToolNameMatchInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidInstance -->

# Class ToolCallValidInstance (1.135.0)

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

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

### ToolCallValidInstance

`ToolCallValidInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.135.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageClassificationPredictionInstance -->

# Class ImageClassificationPredictionInstance (1.135.0)

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes or Cloud Storage URI to make the prediction on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## Methods

### ImageClassificationPredictionInstance

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

### ImageClassificationPredictionInstance

```
ImageClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Classification.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeResponse -->

# Class UpgradeNotebookRuntimeResponse (1.135.0)

```
UpgradeNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.UpgradeNotebookRuntime.

## Methods

### UpgradeNotebookRuntimeResponse

```
UpgradeNotebookRuntimeResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.UpgradeNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchResults -->

# Class ExactMatchResults (1.135.0)

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

## Attribute |
|
|---|---|
Name |
Description |
`exact_match_metric_values` |
`MutableSequence[`
Output only. Exact match metric values. |

## Methods

### ExactMatchResults

`ExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for exact match metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob -->

# Class TuningJob (1.135.0)

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
`name` |
`str`
Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|
`tuned_model_display_name` |
`str`
Optional. The display name of the TunedModel. The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tuned_model_display_name will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version. |
`description` |
`str`
Optional. The description of the TuningJob. |
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
`encryption_spec` |
Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key. |
`service_account` |
`str`
The service account that the tuningJob workload runs as. If not specified, the Vertex AI Secure Fine-Tuned Service Agent in the project will be used. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient -->

# Class SpecialistPoolServiceClient (1.135.0)

```
SpecialistPoolServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### SpecialistPoolServiceClient

```
SpecialistPoolServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the specialist pool service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the SpecialistPoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1.[CreateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateSpecialistPoolRequest.html)(
parent="parent_value",
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[create_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_create_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.CreateSpecialistPool. |
`parent` |
`str`
Required. The parent Project name for the new SpecialistPool. The form is |
`specialist_pool` |
Required. The SpecialistPool to create. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_delete_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.DeleteSpecialistPool. |
`name` |
`str`
Required. The resource name of the SpecialistPool to delete. Format: |
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
`SpecialistPoolServiceClient` |
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
`SpecialistPoolServiceClient` |
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
`SpecialistPoolServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_get_specialist_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SpecialistPoolService.GetSpecialistPool. |
`name` |
`str`
Required. The name of the SpecialistPool resource. The form is |
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
SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console. |

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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager
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
def sample_list_specialist_pools():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSpecialistPoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_specialist_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_list_specialist_pools)(request=request)
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
The request object. Request message for SpecialistPoolService.ListSpecialistPools. |
`parent` |
`str`
Required. The name of the SpecialistPool's parent resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_specialist_pool():
# Create a client
client = aiplatform_v1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1.[UpdateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateSpecialistPoolRequest.html)(
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[update_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1_services_specialist_pool_service_SpecialistPoolServiceClient_update_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.UpdateSpecialistPool. |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient -->

# Class GenAiTuningServiceClient (1.135.0)

```
GenAiTuningServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### GenAiTuningServiceClient

```
GenAiTuningServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the gen ai tuning service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the GenAiTuningServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_cancel_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTuningJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_cancel_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CancelTuningJob. |
`name` |
`str`
Required. The name of the TuningJob to cancel. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_create_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuning_job = aiplatform_v1beta1.[TuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningJob.html)()
tuning_job.base_model = "base_model_value"
tuning_job.supervised_tuning_spec.training_dataset_uri = "training_dataset_uri_value"
request = aiplatform_v1beta1.[CreateTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTuningJobRequest.html)(
parent="parent_value",
tuning_job=tuning_job,
)
# Make the request
response = client.[create_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_create_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.CreateTuningJob. |
`parent` |
`str`
Required. The resource name of the Location to create the TuningJob in. Format: |
`tuning_job` |
Required. The TuningJob to create. This corresponds to the |
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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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
`GenAiTuningServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_get_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GenAiTuningService.GetTuningJob. |
`name` |
`str`
Required. The name of the TuningJob resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager
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
def sample_list_tuning_jobs():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_list_tuning_jobs)(request=request)
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
The request object. Request message for GenAiTuningService.ListTuningJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the TuningJobs from. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_rebase_tuned_model():
# Create a client
client = aiplatform_v1beta1.
```[GenAiTuningServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html)()
# Initialize request argument(s)
tuned_model_ref = aiplatform_v1beta1.[TunedModelRef](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelRef.html)()
tuned_model_ref.tuned_model = "tuned_model_value"
request = aiplatform_v1beta1.[RebaseTunedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelRequest.html)(
parent="parent_value",
tuned_model_ref=tuned_model_ref,
)
# Make the request
operation = client.[rebase_tuned_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.GenAiTuningServiceClient.html#google_cloud_aiplatform_v1beta1_services_gen_ai_tuning_service_GenAiTuningServiceClient_rebase_tuned_model)(request=request)
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
The request object. Request message for GenAiTuningService.RebaseTunedModel. |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: |
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service -->

# Package pipeline_service (1.135.0)

API documentation for `aiplatform_v1.services.pipeline_service`

package.

## Classes

[PipelineServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceAsyncClient)

A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

[PipelineServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.PipelineServiceClient)

A service for creating and managing Vertex AI's pipelines. This
includes both `TrainingPipeline`

resources (used for AutoML and
custom training) and `PipelineJob`

resources (used for Vertex AI
Pipelines).

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers)

API documentation for `aiplatform_v1.services.pipeline_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.RegionalResourceReferences.ReferencesEntry -->

# Class ReferencesEntry (1.135.0)

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ReferencesEntry

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationSpec -->

# Class DistillationSpec (1.135.0)

`DistillationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Distillation.

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
`base_teacher_model` |
`str`
The base teacher model that is being distilled. See `Supported models |
`tuned_teacher_model_source` |
`str`
The resource name of the Tuned teacher model. Format: `projects/{project}/locations/{location}/models/{model}` .
This field is a member of `oneof` _ `teacher_model` .
|
`training_dataset_uri` |
`str`
Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file. |
`validation_dataset_uri` |
`str`
Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file. This field is a member of `oneof` _ `_validation_dataset_uri` .
|
`hyper_parameters` |
Optional. Hyperparameters for Distillation. |
`student_model` |
`str`
The student model that is being tuned, e.g., "google/gemma-2b-1.1-it". |
`pipeline_root_directory` |
`str`
Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the distillation pipeline. It is used by the system to generate the paths of output artifacts. |

## Methods

### DistillationSpec

`DistillationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Distillation.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.DeploymentSpec.ResourceLimitsEntry -->

# Class ResourceLimitsEntry (1.135.0)

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourceLimitsEntry

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.ParameterValuesEntry -->

# Class ParameterValuesEntry (1.135.0)

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ParameterValuesEntry

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.ContentValidationStats -->

# Class ContentValidationStats (1.135.0)

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`valid_record_count` |
`int`
Number of records in this file that were successfully processed. |
`invalid_record_count` |
`int`
Number of records in this file we skipped due to validate errors. |
`partial_errors` |
`MutableSequence[`
The detail information of the partial failures encountered for those invalid records that couldn't be parsed. Up to 50 partial errors will be reported. |
`valid_sparse_record_count` |
`int`
Number of sparse records in this file that were successfully processed. |
`invalid_sparse_record_count` |
`int`
Number of sparse records in this file we skipped due to validate errors. |

## Methods

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.State -->

# Class State (1.135.0)

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Should not be used. |
`DEFAULT` |
The default behavior of whether to enable the monitoring. EntityType-level config: disabled. Feature-level config: inherited from the configuration of EntityType this Feature belongs to. |
`ENABLED` |
Explicitly enables import features analysis. EntityType-level config: by default enables import features analysis for all Features under it. Feature-level config: enables import features analysis regardless of the EntityType-level config. |
`DISABLED` |
Explicitly disables import features analysis. EntityType-level config: by default disables import features analysis for all Features under it. Feature-level config: disables import features analysis regardless of the EntityType-level config. |

## Methods

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig -->

# Class RoutingConfig (1.135.0)

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
`auto_mode` |
Automated routing. This field is a member of `oneof` _ `routing_config` .
|
`manual_mode` |
Manual routing. This field is a member of `oneof` _ `routing_config` .
|

## Classes

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesRequest -->

# Class ReadFeatureValuesRequest (1.135.0)

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the EntityType for the entity being read. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_id` |
`str`
Required. ID for a specific entity. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. |

## Methods

### ReadFeatureValuesRequest

`ReadFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.ReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageObjectDetectionPredictionInstance -->

# Class ImageObjectDetectionPredictionInstance (1.135.0)

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes or Cloud Storage URI to make the prediction on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## Methods

### ImageObjectDetectionPredictionInstance

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

### ImageObjectDetectionPredictionInstance

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Presets.Modality -->

# Class Modality (1.135.0)

`Modality(value)`


Preset option controlling parameters for different modalities

## Enums |
|
|---|---|
Name |
Description |
`MODALITY_UNSPECIFIED` |
Should not be set. Added as a recommended best practice for enums |
`IMAGE` |
IMAGE modality |
`TEXT` |
TEXT modality |
`TABULAR` |
TABULAR modality |

## Methods

### Modality

`Modality(value)`


Preset option controlling parameters for different modalities

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesResponse -->

# Class BatchReadFeatureValuesResponse (1.135.0)

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

## Methods

### BatchReadFeatureValuesResponse

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.MonthlyUsageDataEntry -->

# Class MonthlyUsageDataEntry (1.135.0)

`MonthlyUsageDataEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Neighbor -->

# Class Neighbor (1.135.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.

## Attributes |
|
|---|---|
Name |
Description |
`neighbor_id` |
`str`
Output only. The neighbor id. |
`neighbor_distance` |
`float`
Output only. The neighbor distance. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse.PerMonthUsageData -->

# Class PerMonthUsageData (1.135.0)

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

## Attribute |
|
|---|---|
Name |
Description |
`user_usage_data` |
`MutableSequence[`
Usage data for each user in the given month. |

## Methods

### PerMonthUsageData

`PerMonthUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per month usage data

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.DeploymentSpec.ResourceLimitsEntry -->

# Class ResourceLimitsEntry (1.135.0)

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ResourceLimitsEntry

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsRequest -->

# Class ListDeploymentResourcePoolsRequest (1.135.0)

```
ListDeploymentResourcePoolsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ListDeploymentResourcePools method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of DeploymentResourcePools to return. The service may return fewer than this value. |
`page_token` |
`str`
A page token, received from a previous `ListDeploymentResourcePools` call. Provide this to
retrieve the subsequent page.
When paginating, all other parameters provided to
`ListDeploymentResourcePools` must match the call that
provided the page token.
|

## Methods

### ListDeploymentResourcePoolsRequest

```
ListDeploymentResourcePoolsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ListDeploymentResourcePools method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.RegionalResourceReferences.ReferencesEntry -->

# Class ReferencesEntry (1.135.0)

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ReferencesEntry

`ReferencesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig -->

# Class RoutingConfig (1.135.0)

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
`auto_mode` |
Automated routing. This field is a member of `oneof` _ `routing_config` .
|
`manual_mode` |
Manual routing. This field is a member of `oneof` _ `routing_config` .
|

## Classes

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentResult -->

# Class FulfillmentResult (1.135.0)

`FulfillmentResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Fulfillment score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for fulfillment score. |
`confidence` |
`float`
Output only. Confidence for fulfillment score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### FulfillmentResult

`FulfillmentResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesResponse -->

# Class ImportFeatureValuesResponse (1.135.0)

`ImportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ImportFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`imported_entity_count` |
`int`
Number of entities that have been imported by the operation. |
`imported_feature_value_count` |
`int`
Number of Feature values that have been imported by the operation. |
`invalid_row_count` |
`int`
The number of rows in input source that weren't imported due to either - Not having any featureValues. - Having a null entityId. - Having a null timestamp. - Not being parsable (applicable for CSV sources). |
`timestamp_outside_retention_rows_count` |
`int`
The number rows that weren't ingested due to having feature timestamps outside the retention boundary. |

## Methods

### ImportFeatureValuesResponse

`ImportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ImportFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs.ParameterValuesEntry -->

# Class ParameterValuesEntry (1.135.0)

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ParameterValuesEntry

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.State -->

# Class State (1.135.0)

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Should not be used. |
`DEFAULT` |
The default behavior of whether to enable the monitoring. EntityType-level config: disabled. Feature-level config: inherited from the configuration of EntityType this Feature belongs to. |
`ENABLED` |
Explicitly enables import features analysis. EntityType-level config: by default enables import features analysis for all Features under it. Feature-level config: enables import features analysis regardless of the EntityType-level config. |
`DISABLED` |
Explicitly disables import features analysis. EntityType-level config: by default disables import features analysis for all Features under it. Feature-level config: disables import features analysis regardless of the EntityType-level config. |

## Methods

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata.ContentValidationStats -->

# Class ContentValidationStats (1.135.0)

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`valid_record_count` |
`int`
Number of records in this file that were successfully processed. |
`invalid_record_count` |
`int`
Number of records in this file we skipped due to validate errors. |
`partial_errors` |
`MutableSequence[`
The detail information of the partial failures encountered for those invalid records that couldn't be parsed. Up to 50 partial errors will be reported. |
`valid_sparse_record_count` |
`int`
Number of sparse records in this file that were successfully processed. |
`invalid_sparse_record_count` |
`int`
Number of sparse records in this file we skipped due to validate errors. |

## Methods

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularClassificationPredictionResult -->

# Class TabularClassificationPredictionResult (1.135.0)

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

## Attributes |
|
|---|---|
Name |
Description |
`classes` |
`MutableSequence[str]`
The name of the classes being classified, contains all possible values of the target column. |
`scores` |
`MutableSequence[float]`
The model's confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes. |

## Methods

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session -->

# Class Session (1.135.0)

`Session(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A session contains a set of actions between users and Vertex agents.

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
Optional. Timestamp of when this session is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. Input only. The TTL for this session. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Identifier. The resource name of the session. Format: 'projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}'. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the session was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the session was updated. |
`display_name` |
`str`
Optional. The display name of the session. |
`session_state` |
`google.protobuf.struct_pb2.Struct`
Optional. Session specific memory which stores key conversation points. |
`user_id` |
`str`
Required. Immutable. String id provided by the user |

## Methods

### Session

`Session(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A session contains a set of actions between users and Vertex agents.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SharePointSources.SharePointSource -->

# Class SharePointSource (1.135.0)

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
`sharepoint_folder_path` |
`str`
The path of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`sharepoint_folder_id` |
`str`
The ID of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`drive_name` |
`str`
The name of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`drive_id` |
`str`
The ID of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`client_id` |
`str`
The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All. |
`client_secret` |
The application secret for the app registered in Azure. |
`tenant_id` |
`str`
Unique identifier of the Azure Active Directory Instance. |
`sharepoint_site_name` |
`str`
The name of the SharePoint site to download from. This can be the site name or the site id. |
`file_id` |
`str`
Output only. The SharePoint file id. Output only. |

## Methods

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAlertConfig.EmailAlertConfig -->

# Class EmailAlertConfig (1.135.0)

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Attribute |
|
|---|---|
Name |
Description |
`user_emails` |
`MutableSequence[str]`
The email addresses to send the alert. |

## Methods

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Port -->

# Class Port (1.135.0)

`Port(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a network port in a container.

## Attribute |
|
|---|---|
Name |
Description |
`container_port` |
`int`
The number of the port to expose on the pod's IP address. Must be a valid port number, between 1 and 65535 inclusive. |

## Methods

### Port

`Port(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a network port in a container.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardTimeSeriesDataRequest -->

# Class ReadTensorboardTimeSeriesDataRequest (1.135.0)

```
ReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`max_data_points` |
`int`
The maximum number of TensorboardTimeSeries' data to return. This value should be a positive integer. This value can be set to -1 to return all data. |
`filter` |
`str`
Reads the TensorboardTimeSeries' data that match the filter expression. |

## Methods

### ReadTensorboardTimeSeriesDataRequest

```
ReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient -->

# Class PredictionServiceClient (1.135.0)

```
PredictionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for online predictions and explanations.

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
`PredictionServiceTransport` |
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

### PredictionServiceClient

```
PredictionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the prediction service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PredictionServiceTransport,Callable[..., PredictionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PredictionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### chat_completions

```
chat_completions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.ChatCompletionsRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[google.api.httpbody_pb2.HttpBody]
```


Exposes an OpenAI-compatible endpoint for chat completions.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_chat_completions():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ChatCompletionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ChatCompletionsRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[chat_completions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_chat_completions)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.ChatCompletions] |
`endpoint` |
`str`
Required. The name of the endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
Optional. The prediction input. Supports HTTP headers and arbitrary data payload. This corresponds to the |
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
`Iterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

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

### count_tokens

```
count_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.CountTokensRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.CountTokensResponse
```


Perform a token counting.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_count_tokens():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CountTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CountTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[count_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_count_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.CountTokens. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to perform token counting. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model. This corresponds to the |
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
Response message for PredictionService.CountTokens. |

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

### direct_predict

```
direct_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.DirectPredictRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.DirectPredictResponse
```


Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_direct_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_direct_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.DirectPredict. |
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
Response message for PredictionService.DirectPredict. |

### direct_raw_predict

```
direct_raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.DirectRawPredictRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.DirectRawPredictResponse
```


Perform an unary online prediction request to a gRPC model server for custom containers.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_direct_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_direct_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.DirectRawPredict. |
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
Response message for PredictionService.DirectRawPredict. |

### embed_content

```
embed_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.EmbedContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.content.Content
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.EmbedContentResponse
```


Embed content with multimodal inputs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_embed_content():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[EmbedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentRequest.html)(
)
# Make the request
response = client.[embed_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_embed_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.EmbedContent. |
`model` |
`str`
Required. The name of the publisher model requested to serve the prediction. Format: |
`content` |
Required. Input content to be embedded. Required. This corresponds to the |
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
Response message for PredictionService.EmbedContent. |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### explain

```
explain(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.ExplainRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
parameters: typing.Optional[google.protobuf.struct_pb2.Value] = None,
deployed_model_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.ExplainResponse
```


Perform an online explanation.

If xref_deployed_model_id is specified, the corresponding DeployModel must have xref_explanation_spec populated. If xref_deployed_model_id is not specified, all DeployedModels must have xref_explanation_spec populated.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_explain():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1beta1.[Value](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Value.html)()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[ExplainRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = client.[explain](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_explain)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.Explain. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the explanation. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
`deployed_model_id` |
`str`
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. This corresponds to the |
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
Response message for PredictionService.Explain. |

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
`PredictionServiceClient` |
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
`PredictionServiceClient` |
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
`PredictionServiceClient` |
The constructed client. |

### generate_content

```
generate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1beta1.types.content.Content]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentResponse
```


Generate content with multimodal inputs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_generate_content():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1beta1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1beta1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
response = client.[generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_generate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
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
Response message for [PredictionService.GenerateContent]. |

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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_template_path

`parse_template_path(path: str) -> typing.Dict[str, str]`


Parses a template path into its component segments.

### predict

```
predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.PredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
parameters: typing.Optional[google.protobuf.struct_pb2.Value] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.PredictResponse
```


Perform an online prediction.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1beta1.[Value](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Value.html)()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[PredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = client.[predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.Predict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
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
Response message for PredictionService.Predict. |

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### raw_predict

```
raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.RawPredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api.httpbody_pb2.HttpBody
```


Perform an online prediction with an arbitrary HTTP payload.

The response includes the following HTTP headers:

`X-Vertex-AI-Endpoint-Id`

: ID of the xref_Endpoint that served this prediction.`X-Vertex-AI-Deployed-Model-Id`

: ID of the Endpoint's xref_DeployedModel that served this prediction.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.RawPredict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the |
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
`google.api.httpbody_pb2.HttpBody` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### server_streaming_predict

```
server_streaming_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictRequest,
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictResponse
]
```


Perform a server-side streaming online prediction request for Vertex LLM streaming.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_server_streaming_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[server_streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_server_streaming_predict)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
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
`Iterable[` |
Response message for PredictionService.StreamingPredict. |

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

### stream_direct_predict

```
stream_direct_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectPredictResponse
]
```


Perform a streaming online prediction request to a gRPC model server for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_direct_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamDirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamDirectPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[stream_direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_direct_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamDirectPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
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
`Iterable[` |
Response message for PredictionService.StreamDirectPredict. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectRawPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectRawPredictResponse
]
```


Perform a streaming online prediction request to a gRPC model server for custom containers.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_direct_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamDirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamDirectRawPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[stream_direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_direct_raw_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamDirectRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
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
`Iterable[` |
Response message for PredictionService.StreamDirectRawPredict. |

### stream_generate_content

```
stream_generate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1beta1.types.content.Content]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentResponse
]
```


Generate content with multimodal inputs with streaming support.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_generate_content():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1beta1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1beta1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
stream = client.[stream_generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_generate_content)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
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
`Iterable[` |
Response message for [PredictionService.GenerateContent]. |

### stream_raw_predict

```
stream_raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamRawPredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[google.api.httpbody_pb2.HttpBody]
```


Perform a streaming online prediction with an arbitrary HTTP payload.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[stream_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_raw_predict)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.StreamRawPredict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. This corresponds to the |
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
`Iterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### streaming_predict

```
streaming_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictResponse
]
```


Perform a streaming online prediction request for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_streaming_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamingPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_streaming_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
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
`Iterable[` |
Response message for PredictionService.StreamingPredict. |

### streaming_raw_predict

```
streaming_raw_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingRawPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingRawPredictResponse
]
```


Perform a streaming online prediction request through gRPC.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_streaming_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamingRawPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[streaming_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_streaming_raw_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamingRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
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
`Iterable[` |
Response message for PredictionService.StreamingRawPredict. |

### template_path

`template_path(project: str, location: str, template: str) -> str`


Returns a fully-qualified template string.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient -->

# Class PredictionServiceClient (1.134.0)

```
PredictionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for online predictions and explanations.

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
`PredictionServiceTransport` |
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

### PredictionServiceClient

```
PredictionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.prediction_service.transports.base.PredictionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the prediction service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PredictionServiceTransport,Callable[..., PredictionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PredictionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### chat_completions

```
chat_completions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.ChatCompletionsRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[google.api.httpbody_pb2.HttpBody]
```


Exposes an OpenAI-compatible endpoint for chat completions.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_chat_completions():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ChatCompletionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ChatCompletionsRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[chat_completions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_chat_completions)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.ChatCompletions] |
`endpoint` |
`str`
Required. The name of the endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
Optional. The prediction input. Supports HTTP headers and arbitrary data payload. This corresponds to the |
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
`Iterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

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

### count_tokens

```
count_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.CountTokensRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.CountTokensResponse
```


Perform a token counting.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_count_tokens():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CountTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CountTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[count_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_count_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.CountTokens. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to perform token counting. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model. This corresponds to the |
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
Response message for PredictionService.CountTokens. |

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

### direct_predict

```
direct_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.DirectPredictRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.DirectPredictResponse
```


Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_direct_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_direct_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.DirectPredict. |
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
Response message for PredictionService.DirectPredict. |

### direct_raw_predict

```
direct_raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.DirectRawPredictRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.DirectRawPredictResponse
```


Perform an unary online prediction request to a gRPC model server for custom containers.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_direct_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_direct_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.DirectRawPredict. |
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
Response message for PredictionService.DirectRawPredict. |

### embed_content

```
embed_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.EmbedContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.content.Content
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.EmbedContentResponse
```


Embed content with multimodal inputs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_embed_content():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[EmbedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentRequest.html)(
)
# Make the request
response = client.[embed_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_embed_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.EmbedContent. |
`model` |
`str`
Required. The name of the publisher model requested to serve the prediction. Format: |
`content` |
Required. Input content to be embedded. Required. This corresponds to the |
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
Response message for PredictionService.EmbedContent. |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### explain

```
explain(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.ExplainRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
parameters: typing.Optional[google.protobuf.struct_pb2.Value] = None,
deployed_model_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.ExplainResponse
```


Perform an online explanation.

If xref_deployed_model_id is specified, the corresponding DeployModel must have xref_explanation_spec populated. If xref_deployed_model_id is not specified, all DeployedModels must have xref_explanation_spec populated.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_explain():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1beta1.[Value](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Value.html)()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[ExplainRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = client.[explain](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_explain)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.Explain. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the explanation. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
`deployed_model_id` |
`str`
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. This corresponds to the |
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
Response message for PredictionService.Explain. |

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
`PredictionServiceClient` |
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
`PredictionServiceClient` |
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
`PredictionServiceClient` |
The constructed client. |

### generate_content

```
generate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1beta1.types.content.Content]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentResponse
```


Generate content with multimodal inputs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_generate_content():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1beta1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1beta1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
response = client.[generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_generate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
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
Response message for [PredictionService.GenerateContent]. |

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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_template_path

`parse_template_path(path: str) -> typing.Dict[str, str]`


Parses a template path into its component segments.

### predict

```
predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.PredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
parameters: typing.Optional[google.protobuf.struct_pb2.Value] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.prediction_service.PredictResponse
```


Perform an online prediction.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1beta1.[Value](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Value.html)()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[PredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = client.[predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.Predict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
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
Response message for PredictionService.Predict. |

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### raw_predict

```
raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.RawPredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api.httpbody_pb2.HttpBody
```


Perform an online prediction with an arbitrary HTTP payload.

The response includes the following HTTP headers:

`X-Vertex-AI-Endpoint-Id`

: ID of the xref_Endpoint that served this prediction.`X-Vertex-AI-Deployed-Model-Id`

: ID of the Endpoint's xref_DeployedModel that served this prediction.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.RawPredict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the |
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
`google.api.httpbody_pb2.HttpBody` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### server_streaming_predict

```
server_streaming_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictRequest,
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictResponse
]
```


Perform a server-side streaming online prediction request for Vertex LLM streaming.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_server_streaming_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[server_streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_server_streaming_predict)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
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
`Iterable[` |
Response message for PredictionService.StreamingPredict. |

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

### stream_direct_predict

```
stream_direct_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectPredictResponse
]
```


Perform a streaming online prediction request to a gRPC model server for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_direct_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamDirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamDirectPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[stream_direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_direct_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamDirectPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
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
`Iterable[` |
Response message for PredictionService.StreamDirectPredict. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectRawPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamDirectRawPredictResponse
]
```


Perform a streaming online prediction request to a gRPC model server for custom containers.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_direct_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamDirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamDirectRawPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[stream_direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_direct_raw_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamDirectRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
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
`Iterable[` |
Response message for PredictionService.StreamDirectRawPredict. |

### stream_generate_content

```
stream_generate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1beta1.types.content.Content]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.GenerateContentResponse
]
```


Generate content with multimodal inputs with streaming support.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_generate_content():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1beta1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1beta1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
stream = client.[stream_generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_generate_content)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
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
`Iterable[` |
Response message for [PredictionService.GenerateContent]. |

### stream_raw_predict

```
stream_raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamRawPredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[google.api.httpbody_pb2.HttpBody]
```


Perform a streaming online prediction with an arbitrary HTTP payload.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_stream_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[stream_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_stream_raw_predict)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.StreamRawPredict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. This corresponds to the |
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
`Iterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### streaming_predict

```
streaming_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingPredictResponse
]
```


Perform a streaming online prediction request for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_streaming_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamingPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_streaming_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
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
`Iterable[` |
Response message for PredictionService.StreamingPredict. |

### streaming_raw_predict

```
streaming_raw_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingRawPredictRequest
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
) -> typing.Iterable[
google.cloud.aiplatform_v1beta1.types.prediction_service.StreamingRawPredictResponse
]
```


Perform a streaming online prediction request through gRPC.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_streaming_raw_predict():
# Create a client
client = aiplatform_v1beta1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamingRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1beta1.StreamingRawPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = client.[streaming_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1beta1_services_prediction_service_PredictionServiceClient_streaming_raw_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamingRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
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
`Iterable[` |
Response message for PredictionService.StreamingRawPredict. |

### template_path

`template_path(project: str, location: str, template: str) -> str`


Returns a fully-qualified template string.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient -->

# Class SpecialistPoolServiceClient (1.134.0)

```
SpecialistPoolServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### SpecialistPoolServiceClient

```
SpecialistPoolServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the specialist pool service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the SpecialistPoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1beta1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSpecialistPoolRequest.html)(
parent="parent_value",
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[create_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceClient_create_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.CreateSpecialistPool. |
`parent` |
`str`
Required. The parent Project name for the new SpecialistPool. The form is |
`specialist_pool` |
Required. The SpecialistPool to create. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceClient_delete_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.DeleteSpecialistPool. |
`name` |
`str`
Required. The resource name of the SpecialistPool to delete. Format: |
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
`SpecialistPoolServiceClient` |
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
`SpecialistPoolServiceClient` |
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
`SpecialistPoolServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSpecialistPoolRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceClient_get_specialist_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SpecialistPoolService.GetSpecialistPool. |
`name` |
`str`
Required. The name of the SpecialistPool resource. The form is |
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
SpecialistPool represents customers' own workforce to work on their data labeling jobs. It includes a group of specialist managers and workers. Managers are responsible for managing the workers in this pool as well as customers' data labeling jobs associated with this pool. Customers create specialist pool as well as start data labeling jobs on Cloud, managers and workers handle the jobs using CrowdCompute console. |

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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager
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
def sample_list_specialist_pools():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSpecialistPoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_specialist_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceClient_list_specialist_pools)(request=request)
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
The request object. Request message for SpecialistPoolService.ListSpecialistPools. |
`parent` |
`str`
Required. The name of the SpecialistPool's parent resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_specialist_pool():
# Create a client
client = aiplatform_v1beta1.
```[SpecialistPoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html)()
# Initialize request argument(s)
specialist_pool = aiplatform_v1beta1.[SpecialistPool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpecialistPool.html)()
specialist_pool.name = "name_value"
specialist_pool.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateSpecialistPoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSpecialistPoolRequest.html)(
specialist_pool=specialist_pool,
)
# Make the request
operation = client.[update_specialist_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient.html#google_cloud_aiplatform_v1beta1_services_specialist_pool_service_SpecialistPoolServiceClient_update_specialist_pool)(request=request)
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
The request object. Request message for SpecialistPoolService.UpdateSpecialistPool. |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. This corresponds to the |
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail.ObjectiveStatusEntry -->

# Class ObjectiveStatusEntry (1.134.0)

`ObjectiveStatusEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ObjectiveStatusEntry

`ObjectiveStatusEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse.MonthlyUsageDataEntry -->

# Class MonthlyUsageDataEntry (1.134.0)

`MonthlyUsageDataEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundednessInstance -->

# Class GroundednessInstance (1.134.0)

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

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
`context` |
`str`
Required. Background information provided in context used to compare against the prediction. This field is a member of `oneof` _ `_context` .
|

## Methods

### GroundednessInstance

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.LaunchStage -->

# Class LaunchStage (1.134.0)

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`LAUNCH_STAGE_UNSPECIFIED` |
The model launch stage is unspecified. |
`EXPERIMENTAL` |
Used to indicate the PublisherModel is at Experimental launch stage, available to a small set of customers. |
`PRIVATE_PREVIEW` |
Used to indicate the PublisherModel is at Private Preview launch stage, only available to a small set of customers, although a larger set of customers than an Experimental launch. Previews are the first launch stage used to get feedback from customers. |
`PUBLIC_PREVIEW` |
Used to indicate the PublisherModel is at Public Preview launch stage, available to all customers, although not supported for production workloads. |
`GA` |
Used to indicate the PublisherModel is at GA launch stage, available to all customers and ready for production workload. |

## Methods

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SharePointSources.SharePointSource -->

# Class SharePointSource (1.134.0)

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
`sharepoint_folder_path` |
`str`
The path of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`sharepoint_folder_id` |
`str`
The ID of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`drive_name` |
`str`
The name of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`drive_id` |
`str`
The ID of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`client_id` |
`str`
The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All. |
`client_secret` |
The application secret for the app registered in Azure. |
`tenant_id` |
`str`
Unique identifier of the Azure Active Directory Instance. |
`sharepoint_site_name` |
`str`
The name of the SharePoint site to download from. This can be the site name or the site id. |
`file_id` |
`str`
Output only. The SharePoint file id. Output only. |

## Methods

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsRequest -->

# Class ListDeploymentResourcePoolsRequest (1.134.0)

```
ListDeploymentResourcePoolsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ListDeploymentResourcePools method.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The maximum number of DeploymentResourcePools to return. The service may return fewer than this value. |
`page_token` |
`str`
A page token, received from a previous `ListDeploymentResourcePools` call. Provide this to
retrieve the subsequent page.
When paginating, all other parameters provided to
`ListDeploymentResourcePools` must match the call that
provided the page token.
|

## Methods

### ListDeploymentResourcePoolsRequest

```
ListDeploymentResourcePoolsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ListDeploymentResourcePools method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FulfillmentResult -->

# Class FulfillmentResult (1.134.0)

`FulfillmentResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Fulfillment score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for fulfillment score. |
`confidence` |
`float`
Output only. Confidence for fulfillment score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### FulfillmentResult

`FulfillmentResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fulfillment result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig -->

# Class ModelMonitoringObjectiveConfig (1.134.0)

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset` |
Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified. |
`training_prediction_skew_detection_config` |
The config for skew between training data and prediction data. |
`prediction_drift_detection_config` |
The config for drift of prediction data. |
`explanation_config` |
The config for integrating with Vertex Explainable AI. |

## Classes

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

### TrainingDataset

`TrainingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training Dataset information.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Methods

### ModelMonitoringObjectiveConfig

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PrivateServiceConnectConfig -->

# Class PrivateServiceConnectConfig (1.134.0)

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
`service_attachment` |
`str`
Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect. |

## Methods

### PrivateServiceConnectConfig

`PrivateServiceConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents configuration for private service connect.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesResponse -->

# Class ImportFeatureValuesResponse (1.134.0)

`ImportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ImportFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`imported_entity_count` |
`int`
Number of entities that have been imported by the operation. |
`imported_feature_value_count` |
`int`
Number of Feature values that have been imported by the operation. |
`invalid_row_count` |
`int`
The number of rows in input source that weren't imported due to either - Not having any featureValues. - Having a null entityId. - Having a null timestamp. - Not being parsable (applicable for CSV sources). |
`timestamp_outside_retention_rows_count` |
`int`
The number rows that weren't ingested due to having feature timestamps outside the retention boundary. |

## Methods

### ImportFeatureValuesResponse

`ImportFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ImportFeatureValues.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardTimeSeriesDataRequest -->

# Class ReadTensorboardTimeSeriesDataRequest (1.134.0)

```
ReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`max_data_points` |
`int`
The maximum number of TensorboardTimeSeries' data to return. This value should be a positive integer. This value can be set to -1 to return all data. |
`filter` |
`str`
Reads the TensorboardTimeSeries' data that match the filter expression. |

## Methods

### ReadTensorboardTimeSeriesDataRequest

```
ReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardTimeSeriesData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets.Modality -->

# Class Modality (1.134.0)

`Modality(value)`


Preset option controlling parameters for different modalities

## Enums |
|
|---|---|
Name |
Description |
`MODALITY_UNSPECIFIED` |
Should not be set. Added as a recommended best practice for enums |
`IMAGE` |
IMAGE modality |
`TEXT` |
TEXT modality |
`TABULAR` |
TABULAR modality |

## Methods

### Modality

`Modality(value)`


Preset option controlling parameters for different modalities

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FulfillmentInput -->

# Class FulfillmentInput (1.134.0)

`FulfillmentInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for fulfillment metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for fulfillment score metric. |
`instance` |
Required. Fulfillment instance. |

## Methods

### FulfillmentInput

`FulfillmentInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for fulfillment metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Bigtable -->

# Class Bigtable (1.134.0)

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`auto_scaling` |
Required. Autoscaling config applied to Bigtable Instance. |
`enable_direct_bigtable_access` |
`bool`
Optional. Whether direct access to the Bigtable instance is enabled or not. |
`bigtable_metadata` |
Output only. Metadata of the Bigtable instance. Output only. |
`zone` |
`str`
Optional. The zone where the underlying Bigtable cluster for the primary Bigtable instance will be provisioned. Only the zone must be provided. For example, only "us-central1-a" should be provided. |

## Classes

### AutoScaling

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

## Methods

### Bigtable

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageObjectDetectionPredictionInstance -->

# Class ImageObjectDetectionPredictionInstance (1.134.0)

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes or Cloud Storage URI to make the prediction on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## Methods

### ImageObjectDetectionPredictionInstance

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

### ImageObjectDetectionPredictionInstance

```
ImageObjectDetectionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Object Detection.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore -->

# Class FeatureOnlineStore (1.134.0)

`FeatureOnlineStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

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
`bigtable` |
Contains settings for the Cloud Bigtable instance that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. This field is a member of `oneof` _ `storage_type` .
|
`optimized` |
Contains settings for the Optimized store that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. When choose Optimized storage type, need to set PrivateServiceConnectConfig.enable_private_service_connect to use private endpoint. Otherwise will use public endpoint by default. This field is a member of `oneof` _ `storage_type` .
|
`name` |
`str`
Identifier. Name of the FeatureOnlineStore. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureOnlineStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureOnlineStore was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureOnlineStore. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`state` |
Output only. State of the featureOnlineStore. |
`dedicated_serving_endpoint` |
Optional. The dedicated serving endpoint for this FeatureOnlineStore, which is different from common Vertex service endpoint. |
`encryption_spec` |
Optional. Customer-managed encryption key spec for data storage. If set, online store will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### Bigtable

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### DedicatedServingEndpoint

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.

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

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

### State

`State(value)`


Possible states a featureOnlineStore can have.

## Methods

### FeatureOnlineStore

`FeatureOnlineStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesResponse -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig -->

# Class ModelMonitoringObjectiveConfig (1.134.0)

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset` |
Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified. |
`training_prediction_skew_detection_config` |
The config for skew between training data and prediction data. |
`prediction_drift_detection_config` |
The config for drift of prediction data. |
`explanation_config` |
The config for integrating with Vertex Explainable AI. |

## Classes

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

### TrainingDataset

`TrainingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training Dataset information.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Methods

### ModelMonitoringObjectiveConfig

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.LaunchStage -->

# Class LaunchStage (1.134.0)

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`LAUNCH_STAGE_UNSPECIFIED` |
The model launch stage is unspecified. |
`EXPERIMENTAL` |
Used to indicate the PublisherModel is at Experimental launch stage, available to a small set of customers. |
`PRIVATE_PREVIEW` |
Used to indicate the PublisherModel is at Private Preview launch stage, only available to a small set of customers, although a larger set of customers than an Experimental launch. Previews are the first launch stage used to get feedback from customers. |
`PUBLIC_PREVIEW` |
Used to indicate the PublisherModel is at Public Preview launch stage, available to all customers, although not supported for production workloads. |
`GA` |
Used to indicate the PublisherModel is at GA launch stage, available to all customers and ready for production workload. |

## Methods

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthType -->

# Class AuthType (1.134.0)

`AuthType(value)`


Type of Auth.

## Enums |
|
|---|---|
Name |
Description |
`AUTH_TYPE_UNSPECIFIED` |
No description available. |
`NO_AUTH` |
No Auth. |
`API_KEY_AUTH` |
API Key Auth. |
`HTTP_BASIC_AUTH` |
HTTP Basic Auth. |
`GOOGLE_SERVICE_ACCOUNT_AUTH` |
Google Service Account Auth. |
`OAUTH` |
OAuth auth. |
`OIDC_AUTH` |
OpenID Connect (OIDC) Auth. |

## Methods

### AuthType

`AuthType(value)`


Type of Auth.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardRunDataResponse -->

# Class WriteTensorboardRunDataResponse (1.134.0)

```
WriteTensorboardRunDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardRunData.

## Methods

### WriteTensorboardRunDataResponse

```
WriteTensorboardRunDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.WriteTensorboardRunData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJobSpec -->

# Class CustomJobSpec (1.134.0)

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location which to run If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`worker_pool_specs` |
`MutableSequence[`
Required. The spec of the worker pools including machine type and Docker image. All worker pools except the first one are optional and can be skipped by providing an empty value. |
`scheduling` |
Scheduling options for a CustomJob. |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. If unspecified, the `Vertex AI Custom Code Service Agent |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to which the Job should be peered. For example,
`projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved ip ranges under the VPC network that can be used for this job. If set, we will deploy the job within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for CustomJob. |
`base_output_directory` |
The Cloud Storage location to store the output of this CustomJob or HyperparameterTuningJob. For HyperparameterTuningJob, the baseOutputDirectory of each child CustomJob backing a Trial is set to a subdirectory of name id under its parent HyperparameterTuningJob's baseOutputDirectory. The following Vertex AI environment variables will be passed to containers or python modules when this field is set: For CustomJob: - AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
For CustomJob backing a Trial of HyperparameterTuningJob:
- AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
|
`protected_artifact_location_id` |
`str`
The ID of the location to store protected artifacts. e.g. us-central1. Populate only when the location is different than CustomJob location. List of supported locations: https://cloud.google.com/vertex-ai/docs/general/locations |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`enable_web_access` |
`bool`
Optional. Whether you want Vertex AI to enable `interactive shell access |
`enable_dashboard_access` |
`bool`
Optional. Whether you want Vertex AI to enable access to the customized dashboard in training chief container. If set to `true` , you can access the dashboard at the URIs
given by
CustomJob.web_access_uris
or
Trial.web_access_uris
(within
HyperparameterTuningJob.trials).
|
`experiment` |
`str`
Optional. The Experiment associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}`
|
`experiment_run` |
`str`
Optional. The Experiment Run associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}-{experiment-run-name}`
|
`models` |
`MutableSequence[str]`
Optional. The name of the Model resources for which to generate a mapping to artifact URIs. Applicable only to some of the Google-provided custom jobs. Format: `projects/{project}/locations/{location}/models/{model}`
In order to retrieve a specific version of the model, also
provide the version ID or version alias. Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the "default"
version will be returned. The "default" version alias is
created for the first version of the model, and can be moved
to other versions later on. There will be exactly one
default version.
|

## Methods

### CustomJobSpec

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageClassificationPredictionParams -->

# Class ImageClassificationPredictionParams (1.134.0)

```
ImageClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Classification.

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
The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10. |

## Methods

### ImageClassificationPredictionParams

```
ImageClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Classification.

### ImageClassificationPredictionParams

```
ImageClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Classification.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundednessInstance -->

# Class GroundednessInstance (1.134.0)

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

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
`context` |
`str`
Required. Background information provided in context used to compare against the prediction. This field is a member of `oneof` _ `_context` .
|

## Methods

### GroundednessInstance

`GroundednessInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoClassificationPredictionResult -->

# Class VideoClassificationPredictionResult (1.134.0)

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`type_` |
`str`
The type of the prediction. The requested types can be configured via parameters. This will be one of - segment-classification - shot-classification - one-sec-interval-classification |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentStart' from the input instance, for other types it is the start of a shot or a 1 second interval respectively. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentEnd' from the input instance, for other types it is the end of a shot or a 1 second interval respectively. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |

## Methods

### VideoClassificationPredictionResult

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

### VideoClassificationPredictionResult

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJobSpec -->

# Class CustomJobSpec (1.134.0)

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location which to run If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`worker_pool_specs` |
`MutableSequence[`
Required. The spec of the worker pools including machine type and Docker image. All worker pools except the first one are optional and can be skipped by providing an empty value. |
`scheduling` |
Scheduling options for a CustomJob. |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. If unspecified, the `Vertex AI Custom Code Service Agent |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to which the Job should be peered. For example,
`projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved ip ranges under the VPC network that can be used for this job. If set, we will deploy the job within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for CustomJob. |
`base_output_directory` |
The Cloud Storage location to store the output of this CustomJob or HyperparameterTuningJob. For HyperparameterTuningJob, the baseOutputDirectory of each child CustomJob backing a Trial is set to a subdirectory of name id under its parent HyperparameterTuningJob's baseOutputDirectory. The following Vertex AI environment variables will be passed to containers or python modules when this field is set: For CustomJob: - AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
For CustomJob backing a Trial of HyperparameterTuningJob:
- AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
|
`protected_artifact_location_id` |
`str`
The ID of the location to store protected artifacts. e.g. us-central1. Populate only when the location is different than CustomJob location. List of supported locations: https://cloud.google.com/vertex-ai/docs/general/locations |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`enable_web_access` |
`bool`
Optional. Whether you want Vertex AI to enable `interactive shell access |
`enable_dashboard_access` |
`bool`
Optional. Whether you want Vertex AI to enable access to the customized dashboard in training chief container. If set to `true` , you can access the dashboard at the URIs
given by
CustomJob.web_access_uris
or
Trial.web_access_uris
(within
HyperparameterTuningJob.trials).
|
`experiment` |
`str`
Optional. The Experiment associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}`
|
`experiment_run` |
`str`
Optional. The Experiment Run associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}-{experiment-run-name}`
|
`models` |
`MutableSequence[str]`
Optional. The name of the Model resources for which to generate a mapping to artifact URIs. Applicable only to some of the Google-provided custom jobs. Format: `projects/{project}/locations/{location}/models/{model}`
In order to retrieve a specific version of the model, also
provide the version ID or version alias. Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the "default"
version will be returned. The "default" version alias is
created for the first version of the model, and can be moved
to other versions later on. There will be exactly one
default version.
|

## Methods

### CustomJobSpec

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.

## Attributes |
|
|---|---|
Name |
Description |
`neighbor_id` |
`str`
Output only. The neighbor id. |
`neighbor_distance` |
`float`
Output only. The neighbor distance. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Neighbors for example-based explanations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesResponse -->

# Class BatchReadFeatureValuesResponse (1.134.0)

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

## Methods

### BatchReadFeatureValuesResponse

```
BatchReadFeatureValuesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeaturestoreService.BatchReadFeatureValues.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundednessResult -->

# Class GroundednessResult (1.134.0)

`GroundednessResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Groundedness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for groundedness score. |
`confidence` |
`float`
Output only. Confidence for groundedness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### GroundednessResult

`GroundednessResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for groundedness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValue -->

# Class FeatureValue (1.134.0)

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

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
`bool_value` |
`bool`
Bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_value` |
`float`
Double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_value` |
`int`
Int64 feature value. This field is a member of `oneof` _ `value` .
|
`string_value` |
`str`
String feature value. This field is a member of `oneof` _ `value` .
|
`bool_array_value` |
A list of bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_array_value` |
A list of double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_array_value` |
A list of int64 type feature value. This field is a member of `oneof` _ `value` .
|
`string_array_value` |
A list of string type feature value. This field is a member of `oneof` _ `value` .
|
`bytes_value` |
`bytes`
Bytes feature value. This field is a member of `oneof` _ `value` .
|
`struct_value` |
A struct type feature value. This field is a member of `oneof` _ `value` .
|
`metadata` |
Metadata of feature value. |

## Classes

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Methods

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeConfig -->

# Class RuntimeConfig (1.134.0)

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime configuration to run the extension.

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
`code_interpreter_runtime_config` |
Code execution runtime configurations for code interpreter extension. This field is a member of `oneof` _ `GoogleFirstPartyExtensionConfig` .
|
`vertex_ai_search_runtime_config` |
Runtime configuration for Vertex AI Search extension. This field is a member of `oneof` _ `GoogleFirstPartyExtensionConfig` .
|
`default_params` |
`google.protobuf.struct_pb2.Struct`
Optional. Default parameters that will be set for all the execution of this extension. If specified, the parameter values can be overridden by values in [[ExecuteExtensionRequest.operation_params]] at request time. The struct should be in a form of map with param name as the key and actual param value as the value. E.g. If this operation requires a param "name" to be set to "abc". you can set this to something like {"name": "abc"}. |

## Classes

### CodeInterpreterRuntimeConfig

```
CodeInterpreterRuntimeConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### VertexAISearchRuntimeConfig

`VertexAISearchRuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### RuntimeConfig

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime configuration to run the extension.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularClassificationPredictionResult -->

# Class TabularClassificationPredictionResult (1.134.0)

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

## Attributes |
|
|---|---|
Name |
Description |
`classes` |
`MutableSequence[str]`
The name of the classes being classified, contains all possible values of the target column. |
`scores` |
`MutableSequence[float]`
The model's confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes. |

## Methods

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

### TabularClassificationPredictionResult

```
TabularClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Classification.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Study.State -->

# Class State (1.134.0)

`State(value)`


Describes the Study state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The study state is unspecified. |
`ACTIVE` |
The study is active. |
`INACTIVE` |
The study is stopped due to an internal error. |
`COMPLETED` |
The study is done when the service exhausts the parameter search space or max_trial_count is reached. |

## Methods

### State

`State(value)`


Describes the Study state.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundednessInput -->

# Class GroundednessInput (1.134.0)

`GroundednessInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for groundedness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for groundedness metric. |
`instance` |
Required. Groundedness instance. |

## Methods

### GroundednessInput

`GroundednessInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for groundedness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient -->

# Class GenAiTuningServiceAsyncClient (1.134.0)

```
GenAiTuningServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
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
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport,
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
google.cloud.aiplatform_v1.types.genai_tuning_service.CancelTuningJobRequest,
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
xref_TuningJob.state is
set to `CANCELLED`

.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_cancel_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CancelTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTuningJobRequest.html)(
name="name_value",
)
# Make the request
await client.[cancel_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_cancel_tuning_job)(request=request)


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
google.cloud.aiplatform_v1.types.genai_tuning_service.CreateTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuning_job: typing.Optional[
google.cloud.aiplatform_v1.types.tuning_job.TuningJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tuning_job.TuningJob
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
from google.cloud import aiplatform_v1
async def sample_create_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
tuning_job = aiplatform_v1.[TuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob.html)()
tuning_job.base_model = "base_model_value"
tuning_job.supervised_tuning_spec.training_dataset_uri = "training_dataset_uri_value"
request = aiplatform_v1.[CreateTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTuningJobRequest.html)(
parent="parent_value",
tuning_job=tuning_job,
)
# Make the request
response = await client.[create_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_create_tuning_job)(request=request)
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
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.transports.base.GenAiTuningServiceTransport
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
google.cloud.aiplatform_v1.types.genai_tuning_service.GetTuningJobRequest,
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
) -> google.cloud.aiplatform_v1.types.tuning_job.TuningJob
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
from google.cloud import aiplatform_v1
async def sample_get_tuning_job():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_get_tuning_job)(request=request)
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
google.cloud.aiplatform_v1.types.genai_tuning_service.ListTuningJobsRequest,
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
google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_tuning_jobs():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_list_tuning_jobs)(request=request)
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
google.cloud.aiplatform_v1.types.genai_tuning_service.RebaseTunedModelRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tuned_model_ref: typing.Optional[
google.cloud.aiplatform_v1.types.tuning_job.TunedModelRef
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


Rebase a TunedModel.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_rebase_tuned_model():
# Create a client
client = aiplatform_v1.
```[GenAiTuningServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html)()
# Initialize request argument(s)
tuned_model_ref = aiplatform_v1.[TunedModelRef](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TunedModelRef.html)()
tuned_model_ref.tuned_model = "tuned_model_value"
request = aiplatform_v1.[RebaseTunedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebaseTunedModelRequest.html)(
parent="parent_value",
tuned_model_ref=tuned_model_ref,
)
# Make the request
operation = client.[rebase_tuned_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient.html#google_cloud_aiplatform_v1_services_gen_ai_tuning_service_GenAiTuningServiceAsyncClient_rebase_tuned_model)(request=request)
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient -->

# Class ExtensionRegistryServiceClient (1.134.0)

```
ExtensionRegistryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.extension_registry_service.transports.base.ExtensionRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.extension_registry_service.transports.base.ExtensionRegistryServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Extension registry.

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
`ExtensionRegistryServiceTransport` |
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

### ExtensionRegistryServiceClient

```
ExtensionRegistryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.extension_registry_service.transports.base.ExtensionRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.extension_registry_service.transports.base.ExtensionRegistryServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the extension registry service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ExtensionRegistryServiceTransport,Callable[..., ExtensionRegistryServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ExtensionRegistryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### delete_extension

```
delete_extension(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.DeleteExtensionRequest,
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


Deletes an Extension.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExtensionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceClient_delete_extension)(request=request)
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
The request object. Request message for ExtensionRegistryService.DeleteExtension. |
`name` |
`str`
Required. The name of the Extension resource to be deleted. Format: |
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

### extension_path

`extension_path(project: str, location: str, extension: str) -> str`


Returns a fully-qualified extension string.

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
`ExtensionRegistryServiceClient` |
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
`ExtensionRegistryServiceClient` |
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
`ExtensionRegistryServiceClient` |
The constructed client. |

### get_extension

```
get_extension(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.GetExtensionRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.extension.Extension
```


Gets an Extension.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExtensionRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceClient_get_extension)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ExtensionRegistryService.GetExtension. |
`name` |
`str`
Required. The name of the Extension resource. Format: |
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
Extensions are tools for large language models to access external data, run computations, etc. |

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

### import_extension

```
import_extension(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ImportExtensionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
extension: typing.Optional[
google.cloud.aiplatform_v1beta1.types.extension.Extension
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


Imports an Extension.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_import_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html)()
# Initialize request argument(s)
extension = aiplatform_v1beta1.[Extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Extension.html)()
extension.display_name = "display_name_value"
extension.manifest.name = "name_value"
extension.manifest.description = "description_value"
extension.manifest.api_spec.open_api_yaml = "open_api_yaml_value"
extension.manifest.auth_config.api_key_config.name = "name_value"
extension.manifest.auth_config.api_key_config.api_key_secret = "api_key_secret_value"
extension.manifest.auth_config.api_key_config.http_element_location = "HTTP_IN_COOKIE"
request = aiplatform_v1beta1.[ImportExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportExtensionRequest.html)(
parent="parent_value",
extension=extension,
)
# Make the request
operation = client.[import_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceClient_import_extension)(request=request)
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
The request object. Request message for ExtensionRegistryService.ImportExtension. |
`parent` |
`str`
Required. The resource name of the Location to import the Extension in. Format: |
`extension` |
Required. The Extension to import. This corresponds to the |
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

### list_extensions

```
list_extensions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
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
google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsPager
)
```


Lists Extensions in a location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_extensions():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListExtensionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_extensions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceClient_list_extensions)(request=request)
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
The request object. Request message for ExtensionRegistryService.ListExtensions. |
`parent` |
`str`
Required. The resource name of the Location to list the Extensions from. Format: |
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
Response message for ExtensionRegistryService.ListExtensions Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_extension_path

`parse_extension_path(path: str) -> typing.Dict[str, str]`


Parses a extension path into its component segments.

### parse_secret_version_path

`parse_secret_version_path(path: str) -> typing.Dict[str, str]`


Parses a secret_version path into its component segments.

### parse_service_path

`parse_service_path(path: str) -> typing.Dict[str, str]`


Parses a service path into its component segments.

### secret_version_path

`secret_version_path(project: str, secret: str, secret_version: str) -> str`


Returns a fully-qualified secret_version string.

### service_path

`service_path(project: str, location: str, namespace: str, service: str) -> str`


Returns a fully-qualified service string.

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

### update_extension

```
update_extension(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.UpdateExtensionRequest,
dict,
]
] = None,
*,
extension: typing.Optional[
google.cloud.aiplatform_v1beta1.types.extension.Extension
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
) -> google.cloud.aiplatform_v1beta1.types.extension.Extension
```


Updates an Extension.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html)()
# Initialize request argument(s)
extension = aiplatform_v1beta1.[Extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Extension.html)()
extension.display_name = "display_name_value"
extension.manifest.name = "name_value"
extension.manifest.description = "description_value"
extension.manifest.api_spec.open_api_yaml = "open_api_yaml_value"
extension.manifest.auth_config.api_key_config.name = "name_value"
extension.manifest.auth_config.api_key_config.api_key_secret = "api_key_secret_value"
extension.manifest.auth_config.api_key_config.http_element_location = "HTTP_IN_COOKIE"
request = aiplatform_v1beta1.[UpdateExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExtensionRequest.html)(
extension=extension,
)
# Make the request
response = client.[update_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceClient_update_extension)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ExtensionRegistryService.UpdateExtension. |
`extension` |
Required. The Extension which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Mask specifying which fields to update. Supported fields: :: * |
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
Extensions are tools for large language models to access external data, run computations, etc. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature -->

# Class Feature (1.134.0)

```
Feature(
feature_name: str,
featurestore_id: typing.Optional[str] = None,
entity_type_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed feature resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### entity_type_name

Full qualified resource name of the managed entityType in which this Feature is.

### featurestore_name

Full qualified resource name of the managed featurestore in which this Feature is.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### Feature

```
Feature(
feature_name: str,
featurestore_id: typing.Optional[str] = None,
entity_type_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed feature given a feature resource name or a feature ID.

Example Usage:

```
my_feature = aiplatform.Feature(
feature_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id/features/my_feature_id'
)
or
my_feature = aiplatform.Feature(
feature_name='my_feature_id',
featurestore_id='my_featurestore_id',
entity_type_id='my_entity_type_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`feature_name` |
`str`
Required. A fully-qualified feature resource name or a feature ID. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id/entityTypes/my_entity_type_id/features/my_feature_id" or "my_feature_id" when project and location are initialized or passed, with featurestore_id and entity_type_id passed. |
`featurestore_id` |
`str`
Optional. Featurestore ID of an existing featurestore to retrieve feature from, when feature_name is passed as Feature ID. |
`entity_type_id` |
`str`
Optional. EntityType ID of an existing entityType to retrieve feature from, when feature_name is passed as Feature ID. The EntityType must exist in the Featurestore if provided by the featurestore_id. |
`project` |
`str`
Optional. Project to retrieve feature from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve feature from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Feature. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If only one of featurestore_id or entity_type_id is provided. |

### create

```
create(
feature_id: str,
value_type: str,
entity_type_name: str,
featurestore_id: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.feature.Feature
```


Creates a Feature resource in an EntityType.

Example Usage:

```
my_feature = aiplatform.Feature.create(
feature_id='my_feature_id',
value_type='INT64',
entity_type_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id'
)
or
my_feature = aiplatform.Feature.create(
feature_id='my_feature_id',
value_type='INT64',
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
```


### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### get_entity_type

`get_entity_type() -> google.cloud.aiplatform.featurestore.entity_type.EntityType`


Retrieves the managed entityType in which this Feature is.

### get_featurestore

```
get_featurestore() -> (
google.cloud.aiplatform.featurestore.featurestore.Featurestore
)
```


Retrieves the managed featurestore in which this Feature is.

### list

```
list(
entity_type_name: str,
featurestore_id: typing.Optional[str] = None,
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.featurestore.feature.Feature]
```


Lists existing managed feature resources in an entityType, given an entityType resource name or an entity_type ID.

Example Usage:

```
my_features = aiplatform.Feature.list(
entity_type_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id'
)
or
my_features = aiplatform.Feature.list(
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
Required. A fully-qualified entityType resource name or an entity_type ID of an existing entityType to list features in. The EntityType must exist in the Featurestore if provided by the featurestore_id. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id/entityTypes/my_entity_type_id" or "my_entity_type_id" when project and location are initialized or passed, with featurestore_id passed. |
`featurestore_id` |
`str`
Optional. Featurestore ID of an existing featurestore to list features in, when entity_type_name is passed as entity_type ID. |
`filter` |
`str`
Optional. Lists the Features that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |
`project` |
`str`
Optional. Project to list features in. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to list features in. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to list features. Overrides credentials set in aiplatform.init. |

### search

```
search(
query: typing.Optional[str] = None,
page_size: typing.Optional[int] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.featurestore.feature.Feature]
```


Searches existing managed Feature resources.

Example Usage:

```
my_features = aiplatform.Feature.search()
```


Parameters |
|
|---|---|
Name |
Description |
`query` |
`str`
Optional. Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using |
`page_size` |
`int`
Optional. The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 100 Features will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`project` |
`str`
Optional. Project to list features in. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to list features in. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to list features. Overrides credentials set in aiplatform.init. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.feature.Feature
```


Updates an existing managed feature resource.

Example Usage:

```
my_feature = aiplatform.Feature(
feature_name='my_feature_id',
featurestore_id='my_featurestore_id',
entity_type_id='my_entity_type_id',
)
my_feature.update(
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
Optional. Description of the Feature. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Features. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types -->

# Package instance_v1beta1.types (1.134.0)

API documentation for `instance_v1beta1.types`

package.

## Classes

[ImageClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageClassificationPredictionInstance)

Prediction input format for Image Classification.

[ImageObjectDetectionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageObjectDetectionPredictionInstance)

Prediction input format for Image Object Detection.

[ImageSegmentationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageSegmentationPredictionInstance)

Prediction input format for Image Segmentation.

[TextClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextClassificationPredictionInstance)

Prediction input format for Text Classification.

[TextExtractionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextExtractionPredictionInstance)

Prediction input format for Text Extraction.

[TextSentimentPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextSentimentPredictionInstance)

Prediction input format for Text Sentiment.

[VideoActionRecognitionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoActionRecognitionPredictionInstance)

Prediction input format for Video Action Recognition.

[VideoClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoClassificationPredictionInstance)

Prediction input format for Video Classification.

[VideoObjectTrackingPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoObjectTrackingPredictionInstance)

Prediction input format for Video Object Tracking.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagEmbeddingModelConfig.VertexPredictionEndpoint -->

# Class VertexPredictionEndpoint (1.134.0)

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`
or
`projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}`
|
`model_version_id` |
`str`
Output only. Version ID of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. |

## Methods

### VertexPredictionEndpoint

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseInstance -->

# Class TrajectorySingleToolUseInstance (1.134.0)

```
TrajectorySingleToolUseInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectorySingleToolUse instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|

## Methods

### TrajectorySingleToolUseInstance

```
TrajectorySingleToolUseInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectorySingleToolUse instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec.DataDriftSpec -->

# Class DataDriftSpec (1.134.0)

`DataDriftSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data drift monitoring spec. Data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[str]`
Feature names / Prediction output names interested in monitoring. These should be a subset of the input feature names or prediction output names specified in the monitoring schema. If the field is not specified all features / prediction outputs outlied in the monitoring schema will be used. |
`categorical_metric_type` |
`str`
Supported metrics type: - l_infinity - jensen_shannon_divergence |
`numeric_metric_type` |
`str`
Supported metrics type: - jensen_shannon_divergence |
`default_categorical_alert_condition` |
Default alert condition for all the categorical features. |
`default_numeric_alert_condition` |
Default alert condition for all the numeric features. |
`feature_alert_conditions` |
`MutableMapping[str, `
Per feature alert condition will override default alert condition. |

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

### DataDriftSpec

`DataDriftSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data drift monitoring spec. Data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValue -->

# Class FeatureValue (1.134.0)

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

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
`bool_value` |
`bool`
Bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_value` |
`float`
Double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_value` |
`int`
Int64 feature value. This field is a member of `oneof` _ `value` .
|
`string_value` |
`str`
String feature value. This field is a member of `oneof` _ `value` .
|
`bool_array_value` |
A list of bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_array_value` |
A list of double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_array_value` |
A list of int64 type feature value. This field is a member of `oneof` _ `value` .
|
`string_array_value` |
A list of string type feature value. This field is a member of `oneof` _ `value` .
|
`bytes_value` |
`bytes`
Bytes feature value. This field is a member of `oneof` _ `value` .
|
`struct_value` |
A struct type feature value. This field is a member of `oneof` _ `value` .
|
`metadata` |
Metadata of feature value. |

## Classes

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Methods

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers -->

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
