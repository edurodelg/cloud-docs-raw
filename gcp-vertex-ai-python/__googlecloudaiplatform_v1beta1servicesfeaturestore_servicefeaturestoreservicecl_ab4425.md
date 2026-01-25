---
merged_at: 2026-01-25T21:47:44.373112
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeaturestore_servicefeaturestoreservicecli_95f20b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicefeaturestoreserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient -->

# Class FeaturestoreServiceClient (1.134.0)

```
FeaturestoreServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.BatchCreateFeaturesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateFeatureRequest
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
from google.cloud import aiplatform_v1beta1
def sample_batch_create_features():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1beta1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_batch_create_features)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.BatchReadFeatureValuesRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_batch_read_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
csv_read_instances = aiplatform_v1beta1.[CsvSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CsvSource.html)()
csv_read_instances.gcs_source.uris = ['uris_value1', 'uris_value2']
destination = aiplatform_v1beta1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
entity_type_specs = aiplatform_v1beta1.[EntityTypeSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.EntityTypeSpec.html)()
entity_type_specs.entity_type_id = "entity_type_id_value"
entity_type_specs.feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1beta1.[BatchReadFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.html)(
csv_read_instances=csv_read_instances,
featurestore="featurestore_value",
destination=destination,
entity_type_specs=entity_type_specs,
)
# Make the request
operation = client.[batch_read_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_batch_read_feature_values)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateEntityTypeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
entity_type: typing.Optional[
google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
from google.cloud import aiplatform_v1beta1
def sample_create_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeRequest.html)(
parent="parent_value",
entity_type_id="entity_type_id_value",
)
# Make the request
operation = client.[create_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_create_entity_type)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateFeatureRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature.Feature
] = None,
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
from google.cloud import aiplatform_v1beta1
def sample_create_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_create_feature)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateFeaturestoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
featurestore: typing.Optional[
google.cloud.aiplatform_v1beta1.types.featurestore.Featurestore
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
from google.cloud import aiplatform_v1beta1
def sample_create_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeaturestoreRequest.html)(
parent="parent_value",
featurestore_id="featurestore_id_value",
)
# Make the request
operation = client.[create_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_create_featurestore)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteEntityTypeRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_delete_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEntityTypeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_delete_entity_type)(request=request)
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
The request object. Request message for [FeaturestoreService.DeleteEntityTypes][]. |
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteFeatureRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_delete_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_delete_feature)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteFeatureValuesRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_delete_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
select_entity = aiplatform_v1beta1.SelectEntity()
select_entity.entity_id_selector.csv_source.gcs_source.uris = ['uris_value1', 'uris_value2']
request = aiplatform_v1beta1.[DeleteFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest.html)(
select_entity=select_entity,
entity_type="entity_type_value",
)
# Make the request
operation = client.[delete_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_delete_feature_values)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteFeaturestoreRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_delete_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_delete_featurestore)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.ExportFeatureValuesRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_export_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1beta1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
feature_selector = aiplatform_v1beta1.[FeatureSelector](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelector.html)()
feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1beta1.[ExportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest.html)(
entity_type="entity_type_value",
destination=destination,
feature_selector=feature_selector,
)
# Make the request
operation = client.[export_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_export_feature_values)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.GetEntityTypeRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
from google.cloud import aiplatform_v1beta1
def sample_get_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEntityTypeRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_get_entity_type)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.GetFeatureRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature.Feature
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
from google.cloud import aiplatform_v1beta1
def sample_get_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_get_feature)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.GetFeaturestoreRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.featurestore.Featurestore
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
from google.cloud import aiplatform_v1beta1
def sample_get_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_get_featurestore)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.ImportFeatureValuesRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_import_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
avro_source = aiplatform_v1beta1.[AvroSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AvroSource.html)()
avro_source.gcs_source.uris = ['uris_value1', 'uris_value2']
feature_specs = aiplatform_v1beta1.[FeatureSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest.FeatureSpec.html)()
feature_specs.id = "id_value"
request = aiplatform_v1beta1.[ImportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest.html)(
avro_source=avro_source,
feature_time_field="feature_time_field_value",
entity_type="entity_type_value",
feature_specs=feature_specs,
)
# Make the request
operation = client.[import_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_import_feature_values)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_entity_types():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEntityTypesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_entity_types](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_list_entity_types)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesPager
)
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
from google.cloud import aiplatform_v1beta1
def sample_list_features():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_list_features)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_featurestores():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturestoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_featurestores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_list_featurestores)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesPager
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
from google.cloud import aiplatform_v1beta1
def sample_search_features():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesRequest.html)(
location="location_value",
)
# Make the request
page_result = client.[search_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_search_features)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.UpdateEntityTypeRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[
google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
) -> google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
from google.cloud import aiplatform_v1beta1
def sample_update_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEntityTypeRequest.html)(
)
# Make the request
response = client.[update_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_update_entity_type)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.UpdateFeatureRequest,
dict,
]
] = None,
*,
feature: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature.Feature
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
) -> google.cloud.aiplatform_v1beta1.types.feature.Feature
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
from google.cloud import aiplatform_v1beta1
def sample_update_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest.html)(
)
# Make the request
response = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_update_feature)(request=request)
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.UpdateFeaturestoreRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[
google.cloud.aiplatform_v1beta1.types.featurestore.Featurestore
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
from google.cloud import aiplatform_v1beta1
def sample_update_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreRequest.html)(
)
# Make the request
operation = client.[update_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceClient_update_featurestore)(request=request)
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformcustomcontainertrainingjob______googlecloudaiplatform_v1be_832dc4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformcustomcontainertrainingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob -->

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabeling_d6a0fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabelingd_7dfe73.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabelingda_cb73fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabelingdat_aaa5de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabelingdata_1c500d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigratedatalabelingdatasetconfigmigratedatalabelingannotateddatasetconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig.MigrateDataLabelingAnnotatedDatasetConfig -->

# Class MigrateDataLabelingAnnotatedDatasetConfig (1.134.0)

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.

## Attribute |
|
|---|---|
Name |
Description |
`annotated_dataset` |
`str`
Required. Full resource name of data labeling AnnotatedDataset. Format: `projects/{project}/datasets/{dataset}/annotatedDatasets/{annotated_dataset}` .
|

## Methods

### MigrateDataLabelingAnnotatedDatasetConfig

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbleumetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuMetricValue -->

# Class BleuMetricValue (1.134.0)

`BleuMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Bleu score. This field is a member of `oneof` _ `_score` .
|

## Methods

### BleuMetricValue

`BleuMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletereasoningenginerequest_googlecloudaiplatform_95cd02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletereasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteReasoningEngineRequest -->

# Class DeleteReasoningEngineRequest (1.134.0)

```
DeleteReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.DeleteReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource to be deleted. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`force` |
`bool`
Optional. If set to true, child resources of this reasoning engine will also be deleted. Otherwise, the request will fail with FAILED_PRECONDITION error when the reasoning engine has undeleted child resources. |

## Methods

### DeleteReasoningEngineRequest

```
DeleteReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.DeleteReasoningEngine.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatepersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdatePersistentResourceRequest -->

# Class UpdatePersistentResourceRequest (1.134.0)

```
UpdatePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for UpdatePersistentResource method.

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's `name` field is used to identify
the PersistentResource to update. Format:
`projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Specify the fields to be overwritten in the PersistentResource by the update method. |

## Methods

### UpdatePersistentResourceRequest

```
UpdatePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for UpdatePersistentResource method.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelevaluationslicesliceslicespecsliceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice.SliceSpec.SliceConfig -->

# Class SliceConfig (1.134.0)

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

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
`value` |
A unique specific value for a given feature. Example: `{ "value": { "string_value": "12345" } }`
This field is a member of `oneof` _ `kind` .
|
`range_` |
A range of values for a numerical feature. Example: `{"range":{"low":10000.0,"high":50000.0}}` will capture
12345 and 23334 in the slice.
This field is a member of `oneof` _ `kind` .
|
`all_values` |
`google.protobuf.wrappers_pb2.BoolValue`
If all_values is set to true, then all possible labels of the keyed feature will have another slice computed. Example: `{"all_values":{"value":true}}`
This field is a member of `oneof` _ `kind` .
|

## Methods

### SliceConfig

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeswritetensorboardexperimentdatarequest_googl_76b050.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeswritetensorboardexperimentdatarequest_google_045ccc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeswritetensorboardexperimentdatarequest_googlec_e71f42.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeswritetensorboardexperimentdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WriteTensorboardExperimentDataRequest -->

# Class WriteTensorboardExperimentDataRequest (1.134.0)

```
WriteTensorboardExperimentDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardExperimentData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_experiment` |
`str`
Required. The resource name of the TensorboardExperiment to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`write_run_data_requests` |
`MutableSequence[`
Required. Requests containing per-run TensorboardTimeSeries data to write. |

## Methods

### WriteTensorboardExperimentDataRequest

```
WriteTensorboardExperimentDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardExperimentData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployOperationMetadata -->

# Class DeployOperationMetadata (1.134.0)

`DeployOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for ModelGardenService.Deploy.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`publisher_model` |
`str`
Output only. The name of the model resource. |
`destination` |
`str`
Output only. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`project_number` |
`int`
Output only. The project number where the deploy model request is sent. |
`model_id` |
`str`
Output only. The model id to be used at query time. |

## Methods

### DeployOperationMetadata

`DeployOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for ModelGardenService.Deploy.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescontainerregistrydestination_googlecloudaiplatform_86fcdb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescontainerregistrydestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ContainerRegistryDestination -->

# Class ContainerRegistryDestination (1.134.0)

```
ContainerRegistryDestination(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The Container Registry location for the container image.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri` |
`str`
Required. Container Registry URI of a container image. Only Google Container Registry and Artifact Registry are supported now. Accepted forms: - Google Container Registry path. For example: `gcr.io/projectId/imageName:tag` .
- Artifact Registry path. For example:
`us-central1-docker.pkg.dev/projectId/repoName/imageName:tag` .
If a tag is not specified, "latest" will be used as the
default tag.
|

## Methods

### ContainerRegistryDestination

```
ContainerRegistryDestination(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The Container Registry location for the container image.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportpublishermodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelRequest -->

# Class ExportPublisherModelRequest (1.134.0)

`ExportPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.ExportPublisherModel.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`
|
`destination` |
Required. The target where we are exporting the model weights to |
`parent` |
`str`
Required. The Location to export the model weights from Format: `projects/{project}/locations/{location}`
|

## Methods

### ExportPublisherModelRequest

`ExportPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.ExportPublisherModel.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragcorpus__googlecloudaiplatform_v1beta1typesstudy_6a919a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragcorpus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagCorpus -->

# Class RagCorpus (1.134.0)

`RagCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagCorpus is a RagFile container and a project can have multiple RagCorpora.

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
`vector_db_config` |
Optional. Immutable. The config for the Vector DBs. This field is a member of `oneof` _ `backend_config` .
|
`vertex_ai_search_config` |
Optional. Immutable. The config for the Vertex AI Search. This field is a member of `oneof` _ `backend_config` .
|
`name` |
`str`
Output only. The resource name of the RagCorpus. |
`display_name` |
`str`
Required. The display name of the RagCorpus. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the RagCorpus. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagCorpus was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagCorpus was last updated. |
`corpus_status` |
Output only. RagCorpus state. |
`encryption_spec` |
Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted. |

## Methods

### RagCorpus

`RagCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagCorpus is a RagFile container and a project can have multiple RagCorpora.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudyspecobservationnoise_googlecloudaiplatfo_d23e96.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecobservationnoise.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ObservationNoise -->

# Class ObservationNoise (1.134.0)

`ObservationNoise(value)`


Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.

## Enums |
|
|---|---|
Name |
Description |
`OBSERVATION_NOISE_UNSPECIFIED` |
The default noise level chosen by Vertex AI. |
`LOW` |
Vertex AI assumes that the objective function is (nearly) perfectly reproducible, and will never repeat the same Trial parameters. |
`HIGH` |
Vertex AI will estimate the amount of noise in metric evaluations, it may repeat the same Trial parameters more than once. |

## Methods

### ObservationNoise

`ObservationNoise(value)`


Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeaturemonitorjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorJobRequest -->

# Class CreateFeatureMonitorJobRequest (1.134.0)

```
CreateFeatureMonitorJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [FeatureRegistryService.CreateFeatureMonitorJobRequest][].

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of FeatureMonitor to create FeatureMonitorJob. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}`
|
`feature_monitor_job` |
Required. The Monitor to create. |
`feature_monitor_job_id` |
`int`
Optional. Output only. System-generated ID for feature monitor job. |

## Methods

### CreateFeatureMonitorJobRequest

```
CreateFeatureMonitorJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [FeatureRegistryService.CreateFeatureMonitorJobRequest][].


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesfeaturenoisesigma_googlecloudaiplatform_v1types_8d539f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeaturenoisesigma_googlecloudaiplatform_v1typest_cd7f27.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeaturenoisesigma_googlecloudaiplatform_v1typestu_cabd71.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturenoisesigma_googlecloudaiplatform_v1typestun_55f23e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturenoisesigma.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureNoiseSigma -->

# Class FeatureNoiseSigma (1.134.0)

`FeatureNoiseSigma(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma by features. Noise sigma represents the standard deviation of the gaussian kernel that will be used to add noise to interpolated inputs prior to computing gradients.

## Attribute |
|
|---|---|
Name |
Description |
`noise_sigma` |
`MutableSequence[`
Noise sigma per feature. No noise is added to features that are not set. |

## Classes

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Methods

### FeatureNoiseSigma

`FeatureNoiseSigma(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma by features. Noise sigma represents the standard deviation of the gaussian kernel that will be used to add noise to interpolated inputs prior to computing gradients.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestuningdatastats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningDataStats -->

# Class TuningDataStats (1.134.0)

`TuningDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The tuning data statistic values for TuningJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`supervised_tuning_data_stats` |
The SFT Tuning data stats. This field is a member of `oneof` _ `tuning_data_stats` .
|

## Methods

### TuningDataStats

`TuningDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The tuning data statistic values for TuningJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescontainerregistrydestination_googlecloudaipla_419863.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontainerregistrydestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContainerRegistryDestination -->

# Class ContainerRegistryDestination (1.134.0)

```
ContainerRegistryDestination(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The Container Registry location for the container image.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri` |
`str`
Required. Container Registry URI of a container image. Only Google Container Registry and Artifact Registry are supported now. Accepted forms: - Google Container Registry path. For example: `gcr.io/projectId/imageName:tag` .
- Artifact Registry path. For example:
`us-central1-docker.pkg.dev/projectId/repoName/imageName:tag` .
If a tag is not specified, "latest" will be used as the
default tag.
|

## Methods

### ContainerRegistryDestination

```
ContainerRegistryDestination(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The Container Registry location for the container image.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprebuiltvoiceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PrebuiltVoiceConfig -->

# Class PrebuiltVoiceConfig (1.134.0)

`PrebuiltVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a prebuilt voice.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`voice_name` |
`str`
The name of the prebuilt voice to use. This field is a member of `oneof` _ `_voice_name` .
|

## Methods

### PrebuiltVoiceConfig

`PrebuiltVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a prebuilt voice.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdataitem__googlecloudaiplatform_v1typespairwi_4796e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdataitem.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataItem -->

# Class DataItem (1.134.0)

`DataItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A piece of data in a Dataset. Could be an image, a video, a document or plain text.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the DataItem. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataItem was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataItem was last updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your DataItems. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one DataItem(System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`payload` |
`google.protobuf.struct_pb2.Value`
Required. The data that the DataItem represents (for example, an image or a text snippet). The schema of the payload is stored in the parent Dataset's [metadata schema's][google.cloud.aiplatform.v1beta1.Dataset.metadata_schema_uri] dataItemSchemaUri field. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
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

### DataItem

`DataItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A piece of data in a Dataset. Could be an image, a video, a document or plain text.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespairwisemetricspec_googlecloudaiplatform_v1typesre_158b2f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespairwisemetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseMetricSpec -->

# Class PairwiseMetricSpec (1.134.0)

`PairwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`metric_prompt_template` |
`str`
Required. Metric prompt template for pairwise metric. This field is a member of `oneof` _ `_metric_prompt_template` .
|

## Methods

### PairwiseMetricSpec

`PairwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecpackagespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.PackageSpec -->

# Class PackageSpec (1.134.0)

`PackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User-provided package specification, containing pickled object and package requirements.

## Attributes |
|
|---|---|
Name |
Description |
`pickle_object_gcs_uri` |
`str`
Optional. The Cloud Storage URI of the pickled python object. |
`dependency_files_gcs_uri` |
`str`
Optional. The Cloud Storage URI of the dependency files in tar.gz format. |
`requirements_gcs_uri` |
`str`
Optional. The Cloud Storage URI of the `requirements.txt`
file
|
`python_version` |
`str`
Optional. The Python version. Supported values are 3.9, 3.10, 3.11, 3.12, 3.13. If not specified, the default value is 3.10. |

## Methods

### PackageSpec

`PackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User-provided package specification, containing pickled object and package requirements.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicespersistent_resource_service_googlecloudaiplat_224b93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicespersistent_resource_service_googlecloudaiplatf_9ec44e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicespersistent_resource_service_googlecloudaiplatfo_ed640d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespersistent_resource_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service -->

# Package persistent_resource_service (1.134.0)

API documentation for `aiplatform_v1.services.persistent_resource_service`

package.

## Classes

[PersistentResourceServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient)

A service for managing Vertex AI's machine learning PersistentResource.

[PersistentResourceServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient)

A service for managing Vertex AI's machine learning PersistentResource.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers)

API documentation for `aiplatform_v1.services.persistent_resource_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExecutionRequest -->

# Class UpdateExecutionRequest (1.134.0)

`UpdateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateExecution.

## Attributes |
|
|---|---|
Name |
Description |
`execution` |
Required. The Execution containing updates. The Execution's Execution.name field is used to identify the Execution to be updated. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. |
`allow_missing` |
`bool`
If set to true, and the Execution is not found, a new Execution is created. |

## Methods

### UpdateExecutionRequest

`UpdateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateExecution.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeployoperationmetadata_googlecloudaiplatform_93672e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployOperationMetadata -->

# Class DeployOperationMetadata (1.134.0)

`DeployOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for ModelGardenService.Deploy.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`publisher_model` |
`str`
Output only. The name of the model resource. |
`destination` |
`str`
Output only. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`project_number` |
`int`
Output only. The project number where the deploy model request is sent. |
`model_id` |
`str`
Output only. The model id to be used at query time. |

## Methods

### DeployOperationMetadata

`DeployOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for ModelGardenService.Deploy.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletereasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteReasoningEngineRequest -->

# Class DeleteReasoningEngineRequest (1.134.0)

```
DeleteReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.DeleteReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource to be deleted. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`force` |
`bool`
Optional. If set to true, child resources of this reasoning engine will also be deleted. Otherwise, the request will fail with FAILED_PRECONDITION error when the reasoning engine has undeleted child resources. |

## Methods

### DeleteReasoningEngineRequest

```
DeleteReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.DeleteReasoningEngine.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_registry_service_googlecloudaipla_6b8d30.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_registry_service_googlecloudaiplat_9a2bd1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service -->

# Package feature_registry_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.feature_registry_service`

package.

## Classes

[FeatureRegistryServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient)

The service that handles CRUD and List for resources for FeatureRegistry.

[FeatureRegistryServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient)

The service that handles CRUD and List for resources for FeatureRegistry.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers)

API documentation for `aiplatform_v1beta1.services.feature_registry_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesresourceruntimespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResourceRuntimeSpec -->

# Class ResourceRuntimeSpec (1.134.0)

`ResourceRuntimeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the runtime on a PersistentResource instance, including but not limited to:

- Service accounts used to run the workloads.
- Whether to make it a dedicated Ray Cluster.

## Attributes |
|
|---|---|
Name |
Description |
`service_account_spec` |
Optional. Configure the use of workload identity on the PersistentResource |
`ray_spec` |
Optional. Ray cluster configuration. Required when creating a dedicated RayCluster on the PersistentResource. |

## Methods

### ResourceRuntimeSpec

`ResourceRuntimeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the runtime on a PersistentResource instance, including but not limited to:

- Service accounts used to run the workloads.
- Whether to make it a dedicated Ray Cluster.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatepersistentresourcerequest_googlecloudai_9fe3b6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatepersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceRequest -->

# Class UpdatePersistentResourceRequest (1.134.0)

```
UpdatePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for UpdatePersistentResource method.

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's `name` field is used to identify
the PersistentResource to update. Format:
`projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Specify the fields to be overwritten in the PersistentResource by the update method. |

## Methods

### UpdatePersistentResourceRequest

```
UpdatePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for UpdatePersistentResource method.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecobservationnoise.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ObservationNoise -->

# Class ObservationNoise (1.134.0)

`ObservationNoise(value)`


Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.

## Enums |
|
|---|---|
Name |
Description |
`OBSERVATION_NOISE_UNSPECIFIED` |
The default noise level chosen by Vertex AI. |
`LOW` |
Vertex AI assumes that the objective function is (nearly) perfectly reproducible, and will never repeat the same Trial parameters. |
`HIGH` |
Vertex AI will estimate the amount of noise in metric evaluations, it may repeat the same Trial parameters more than once. |

## Methods

### ObservationNoise

`ObservationNoise(value)`


Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicefeaturestoreserviceasynccli_06046b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicefeaturestoreserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient -->

# Class FeaturestoreServiceAsyncClient (1.134.0)

```
FeaturestoreServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### FeaturestoreServiceAsyncClient

```
FeaturestoreServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the featurestore service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeaturestoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_batch_create_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_batch_create_features)(request=request)
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
The request object. Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures. |
`parent` |
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: |
`requests` |
`:class:`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_batch_read_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
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
operation = client.[batch_read_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_batch_read_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.BatchReadFeatureValues. |
`featurestore` |
Required. The resource name of the Featurestore from which to query Feature values. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEntityTypeRequest.html)(
parent="parent_value",
entity_type_id="entity_type_id_value",
)
# Make the request
operation = client.[create_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_create_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.CreateEntityType. |
`parent` |
Required. The resource name of the Featurestore to create EntityTypes. Format: |
`entity_type` |
The EntityType to create. This corresponds to the |
`entity_type_id` |
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_create_feature)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature. |
`parent` |
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: |
`feature` |
Required. The Feature to create. This corresponds to the |
`feature_id` |
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeaturestoreRequest.html)(
parent="parent_value",
featurestore_id="featurestore_id_value",
)
# Make the request
operation = client.[create_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_create_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeaturestore. |
`parent` |
Required. The resource name of the Location to create Featurestores. Format: |
`featurestore` |
Required. The Featurestore to create. This corresponds to the |
`featurestore_id` |
Required. The ID to use for this Featurestore, which will become the final component of the Featurestore's resource name. This value may be up to 60 characters, and valid characters are |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEntityTypeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteEntityType. |
`name` |
Required. The name of the EntityType to be deleted. Format: |
`force` |
If set to true, any Features for this EntityType will also be deleted. (Otherwise, the request will only work if the EntityType has no Features.) This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_feature)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature. |
`name` |
Required. The name of the Features to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
select_entity = aiplatform_v1.SelectEntity()
select_entity.entity_id_selector.csv_source.gcs_source.uris = ['uris_value1', 'uris_value2']
request = aiplatform_v1.[DeleteFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest.html)(
select_entity=select_entity,
entity_type="entity_type_value",
)
# Make the request
operation = client.[delete_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeatureValues. |
`entity_type` |
Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeaturestore. |
`name` |
Required. The name of the Featurestore to be deleted. Format: |
`force` |
If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.) This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_export_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
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
operation = client.[export_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_export_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ExportFeatureValues. |
`entity_type` |
Required. The resource name of the EntityType from which to export Feature values. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`FeaturestoreServiceAsyncClient` |
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
`FeaturestoreServiceAsyncClient` |
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
`FeaturestoreServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEntityTypeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_get_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.GetEntityType. |
`name` |
Required. The name of the EntityType resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_get_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature. |
`name` |
Required. The name of the Feature resource. Format for entity_type as parent: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_get_featurestore)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.GetFeaturestore. |
`name` |
Required. The name of the Featurestore resource. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_import_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
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
operation = client.[import_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_import_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ImportFeatureValues. |
`entity_type` |
Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesAsyncPager
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
async def sample_list_entity_types():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEntityTypesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_entity_types](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_list_entity_types)(request=request)
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
The request object. Request message for FeaturestoreService.ListEntityTypes. |
`parent` |
Required. The resource name of the Featurestore to list EntityTypes. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesAsyncPager
)
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
async def sample_list_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_list_features)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures. |
`parent` |
Required. The resource name of the Location to list Features. Format for entity_type as parent: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager
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
async def sample_list_featurestores():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturestoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_featurestores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_list_featurestores)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeaturestores. |
`parent` |
Required. The resource name of the Location to list Featurestores. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesAsyncPager
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
async def sample_search_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesRequest.html)(
location="location_value",
)
# Make the request
page_result = client.[search_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_search_features)(request=request)
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
The request object. Request message for FeaturestoreService.SearchFeatures. |
`location` |
Required. The resource name of the Location to search Features. Format: |
`query` |
Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_update_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEntityTypeRequest.html)(
)
# Make the request
response = await client.[update_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_update_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.UpdateEntityType. |
`entity_type` |
Required. The EntityType's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_update_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureRequest.html)(
)
# Make the request
response = await client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_update_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature. |
`feature` |
Required. The Feature's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_update_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeaturestoreRequest.html)(
)
# Make the request
operation = client.[update_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceAsyncClient_update_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.UpdateFeaturestore. |
`featurestore` |
Required. The Featurestore's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesindex_serviceindexserviceasyncclient_______7c290f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_serviceindexserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient -->

# Class IndexServiceAsyncClient (1.134.0)

```
IndexServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### IndexServiceAsyncClient

```
IndexServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_create_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
index = aiplatform_v1beta1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexRequest.html)(
parent="parent_value",
index=index,
)
# Make the request
operation = client.[create_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_create_index)(request=request)
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
The request object. Request message for IndexService.CreateIndex. |
`parent` |
Required. The resource name of the Location to create the Index in. Format: |
`index` |
Required. The Index to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_delete_index)(request=request)
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
The request object. Request message for IndexService.DeleteIndex. |
`name` |
Required. The name of the Index resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`IndexServiceAsyncClient` |
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
`IndexServiceAsyncClient` |
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
`IndexServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_get_index)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.GetIndex |
`name` |
Required. The name of the Index resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_import_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
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
operation = client.[import_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_import_index)(request=request)
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
The request object. Request message for IndexService.ImportIndex. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesAsyncPager
)
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
async def sample_list_indexes():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListIndexesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_indexes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_list_indexes)(request=request)
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
The request object. Request message for IndexService.ListIndexes. |
`parent` |
Required. The resource name of the Location from which to list the Indexes. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_remove_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RemoveDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = await client.[remove_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_remove_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.RemoveDatapoints |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_update_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
index = aiplatform_v1beta1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexRequest.html)(
index=index,
)
# Make the request
operation = client.[update_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_update_index)(request=request)
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
The request object. Request message for IndexService.UpdateIndex. |
`index` |
Required. The Index which updates the resource on the server. This corresponds to the |
`update_mask` |
The update mask applies to the resource. For the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_upsert_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpsertDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = await client.[upsert_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceAsyncClient_upsert_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.UpsertDatapoints |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesmodelevaluationsliceslice_googlecloudaiplatfor_8955ca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesmodelevaluationsliceslice_googlecloudaiplatform_96b8cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmodelevaluationsliceslice_googlecloudaiplatform__9f4f63.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelevaluationsliceslice_googlecloudaiplatform_v_083f4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelevaluationsliceslice_googlecloudaiplatform_v1_752034.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelevaluationsliceslice.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelEvaluationSlice.Slice -->

# Class Slice (1.134.0)

`Slice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Definition of a slice.

## Attributes |
|
|---|---|
Name |
Description |
`dimension` |
`str`
Output only. The dimension of the slice. Well-known dimensions are: - `annotationSpec` : This slice is on the test data that
has either ground truth or prediction with
AnnotationSpec.display_name
equals to
value.
- `slice` : This slice is a user customized slice defined
by its SliceSpec.
|
`value` |
`str`
Output only. The value of the dimension in this slice. |
`slice_spec` |
Output only. Specification for how the data was sliced. |

## Classes

### SliceSpec

`SliceSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for how the data should be sliced.

## Methods

### Slice

`Slice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Definition of a slice.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborqueryparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.Parameters -->

# Class Parameters (1.134.0)

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided in each query to tune query latency and recall.

## Attributes |
|
|---|---|
Name |
Description |
`approximate_neighbor_candidates` |
`int`
Optional. The number of neighbors to find via approximate search before exact reordering is performed; if set, this value must be > neighbor_count. |
`leaf_nodes_search_fraction` |
`float`
Optional. The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0. |

## Methods

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided in each query to tune query latency and recall.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespersistentresourcestate_googlecloudaiplatform_v1be_6e8ac0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespersistentresourcestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentResource.State -->

# Class State (1.134.0)

`State(value)`


Describes the PersistentResource state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Not set. |
`PROVISIONING` |
The PROVISIONING state indicates the persistent resources is being created. |
`RUNNING` |
The RUNNING state indicates the persistent resource is healthy and fully usable. |
`STOPPING` |
The STOPPING state indicates the persistent resource is being deleted. |
`ERROR` |
The ERROR state indicates the persistent resource may be unusable. Details can be found in the `error` field. |
`REBOOTING` |
The REBOOTING state indicates the persistent resource is being rebooted (PR is not available right now but is expected to be ready again later). |
`UPDATING` |
The UPDATING state indicates the persistent resource is being updated. |

## Methods

### State

`State(value)`


Describes the PersistentResource state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExecutionRequest -->

# Class UpdateExecutionRequest (1.134.0)

`UpdateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateExecution.

## Attributes |
|
|---|---|
Name |
Description |
`execution` |
Required. The Execution containing updates. The Execution's Execution.name field is used to identify the Execution to be updated. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. |
`allow_missing` |
`bool`
If set to true, and the Execution is not found, a new Execution is created. |

## Methods

### UpdateExecutionRequest

`UpdateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateExecution.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesschedule_service_googlecloudaiplatform_v1_e36d74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesschedule_service_googlecloudaiplatform_v1t_4f788b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesschedule_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service -->

# Package schedule_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.schedule_service`

package.

## Classes

[ScheduleServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceAsyncClient)

A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

[ScheduleServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.ScheduleServiceClient)

A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers)

API documentation for `aiplatform_v1beta1.services.schedule_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesenvvar.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EnvVar -->

# Class EnvVar (1.134.0)

`EnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable present in a Container or Python Module.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name of the environment variable. Must be a valid C identifier. |
`value` |
`str`
Required. Variables that reference a $(VAR_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |

## Methods

### EnvVar

`EnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable present in a Container or Python Module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1typesvideoclassificationpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoClassificationPredictionParams -->

# Class VideoClassificationPredictionParams (1.134.0)

```
VideoClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Classification.

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
The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000. |
`segment_classification` |
`bool`
Set to true to request segment-level classification. Vertex AI returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true |
`shot_classification` |
`bool`
Set to true to request shot-level classification. Vertex AI determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Vertex AI then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false |
`one_sec_interval_classification` |
`bool`
Set to true to request classification for a video at one-second intervals. Vertex AI returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false |

## Methods

### VideoClassificationPredictionParams

```
VideoClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Classification.

### VideoClassificationPredictionParams

```
VideoClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Classification.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescreatepipelinejobrequest_googlecloudaiplatform_v_ccd925.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreatepipelinejobrequest_googlecloudaiplatform_v1_9dc41f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatepipelinejobrequest_googlecloudaiplatform_v1t_da1bf3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatepipelinejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePipelineJobRequest -->

# Class CreatePipelineJobRequest (1.134.0)

`CreatePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.CreatePipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`
|
`pipeline_job` |
Required. The PipelineJob to create. |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreatePipelineJobRequest

`CreatePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.CreatePipelineJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewsyncsyncsummary.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewSync.SyncSummary -->

# Class SyncSummary (1.134.0)

`SyncSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.

## Attributes |
|
|---|---|
Name |
Description |
`row_synced` |
`int`
Output only. Total number of rows synced. |
`total_slot` |
`int`
Output only. BigQuery slot milliseconds consumed for the sync job. |
`system_watermark_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Lower bound of the system time watermark for the sync job. This is only set for continuously syncing feature views. |

## Methods

### SyncSummary

`SyncSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexactmatchmetricvalue_googlecloudaiplatform_v1beta_8c9d0a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexactmatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExactMatchMetricValue -->

# Class ExactMatchMetricValue (1.134.0)

`ExactMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Exact match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Exact match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ExactMatchMetricValue

`ExactMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Exact match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureOnlineStoreRequest -->

# Class DeleteFeatureOnlineStoreRequest (1.134.0)

```
DeleteFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureOnlineStore to be deleted. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`force` |
`bool`
If set to true, any FeatureViews and Features for this FeatureOnlineStore will also be deleted. (Otherwise, the request will only work if the FeatureOnlineStore has no FeatureViews.) |

## Methods

### DeleteFeatureOnlineStoreRequest

```
DeleteFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexecutablecode_googlecloudaiplatform_v1types_067482.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexecutablecode_googlecloudaiplatform_v1typesr_29e6fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexecutablecode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecutableCode -->

# Class ExecutableCode (1.134.0)

`ExecutableCode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [FunctionDeclaration] tool and [FunctionCallingConfig] mode is set to [Mode.CODE].

## Attributes |
|
|---|---|
Name |
Description |
`language` |
Required. Programming language of the `code` .
|
`code` |
`str`
Required. The code to be executed. |

## Classes

### Language

`Language(value)`


Supported programming languages for the generated code.

## Methods

### ExecutableCode

`ExecutableCode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [FunctionDeclaration] tool and [FunctionCallingConfig] mode is set to [Mode.CODE].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragretrievalconfigrankingrankservice.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagRetrievalConfig.Ranking.RankService -->

# Class RankService (1.134.0)

`RankService(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Rank Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`
This field is a member of `oneof` _ `_model_name` .
|

## Methods

### RankService

`RankService(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Rank Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnasjobspecmultitrialalgorithmspecsearchtrials_cfcdcd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnasjobspecmultitrialalgorithmspecsearchtrialspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec.SearchTrialSpec -->

# Class SearchTrialSpec (1.134.0)

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.

## Attributes |
|
|---|---|
Name |
Description |
`search_trial_job_spec` |
Required. The spec of a search trial job. The same spec applies to all search trials. |
`max_trial_count` |
`int`
Required. The maximum number of Neural Architecture Search (NAS) trials to run. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`max_failed_trial_count` |
`int`
The number of failed trials that need to be seen before failing the NasJob. If set to 0, Vertex AI decides how many trials must fail before the whole job fails. |

## Methods

### SearchTrialSpec

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexecutablecode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExecutableCode -->

# Class ExecutableCode (1.134.0)

`ExecutableCode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [FunctionDeclaration] tool and [FunctionCallingConfig] mode is set to [Mode.CODE].

## Attributes |
|
|---|---|
Name |
Description |
`language` |
Required. Programming language of the `code` .
|
`code` |
`str`
Required. The code to be executed. |

## Classes

### Language

`Language(value)`


Supported programming languages for the generated code.

## Methods

### ExecutableCode

`ExecutableCode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [FunctionDeclaration] tool and [FunctionCallingConfig] mode is set to [Mode.CODE].


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistnotebookruntimetemplatesrequest_googleclouda_47db02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistnotebookruntimetemplatesrequest_googlecloudai_dfa31b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistnotebookruntimetemplatesrequest_googlecloudaip_553433.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnotebookruntimetemplatesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesRequest -->

# Class ListNotebookRuntimeTemplatesRequest (1.134.0)

```
ListNotebookRuntimeTemplatesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.ListNotebookRuntimeTemplates.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookRuntimeTemplate` supports = and !=.
`notebookRuntimeTemplate` represents the
NotebookRuntimeTemplate ID, i.e. the last segment of the
NotebookRuntimeTemplate's [resource name]
[google.cloud.aiplatform.v1.NotebookRuntimeTemplate.name].
- `display_name` supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `notebookRuntimeType` supports = and !=.
notebookRuntimeType enum: [USER_DEFINED, ONE_CLICK].
- `machineType` supports = and !=.
- `acceleratorType` supports = and !=.
Some examples:
- `notebookRuntimeTemplate=notebookRuntimeTemplate123`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `notebookRuntimeType=USER_DEFINED`
- `machineType=e2-standard-4`
- `acceleratorType=NVIDIA_TESLA_T4`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookRuntimeTemplatesResponse.next_page_token of the previous NotebookService.ListNotebookRuntimeTemplates call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListNotebookRuntimeTemplatesRequest

```
ListNotebookRuntimeTemplatesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.ListNotebookRuntimeTemplates.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesqueryartifactlineagesubgraphrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryArtifactLineageSubgraphRequest -->

# Class QueryArtifactLineageSubgraphRequest (1.134.0)

```
QueryArtifactLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryArtifactLineageSubgraph.

## Attributes |
|
|---|---|
Name |
Description |
`artifact` |
`str`
Required. The resource name of the Artifact whose Lineage needs to be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
The request may error with FAILED_PRECONDITION if the number
of Artifacts, the number of Executions, or the number of
Events that would be returned for the Context exceeds 1000.
|
`max_hops` |
`int`
Specifies the size of the lineage graph in terms of number of hops from the specified artifact. Negative Value: INVALID_ARGUMENT error is returned 0: Only input artifact is returned. No value: Transitive closure is performed to return the complete graph. |
`filter` |
`str`
Filter specifying the boolean condition for the Artifacts to satisfy in order to be part of the Lineage Subgraph. The syntax to define filter query is based on https://google.aip.dev/160. The supported set of filters include the following: - **Attribute filtering**: For example: `display_name = "test"` Supported fields include:
`name` , `display_name` , `uri` , `state` ,
`schema_title` , `create_time` , and `update_time` .
Time fields, such as `create_time` and `update_time` ,
require values specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"`
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` . For example:
`metadata.field_1.number_value = 10.0` In case the field
name contains special characters (such as colon), one can
embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
Each of the above supported filter types can be combined
together using logical operators (`AND` & `OR` ). Maximum
nested expression depth allowed is 5.
For example:
`display_name = "test" AND metadata.field1.bool_value = true` .
|

## Methods

### QueryArtifactLineageSubgraphRequest

```
QueryArtifactLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryArtifactLineageSubgraph.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessearchmodelmonitoringalertsresponse_googlecl_89e925.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchmodelmonitoringalertsresponse_googleclo_1e8bd9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodelmonitoringalertsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsResponse -->

# Class SearchModelMonitoringAlertsResponse (1.134.0)

```
SearchModelMonitoringAlertsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.SearchModelMonitoringAlerts.

## Attributes |
|
|---|---|
Name |
Description |
`model_monitoring_alerts` |
`MutableSequence[`
Alerts retrieved for the requested objectives. Sorted by alert time descendingly. |
`total_number_alerts` |
`int`
The total number of alerts retrieved by the requested objectives. |
`next_page_token` |
`str`
The page token that can be used by the next ModelMonitoringService.SearchModelMonitoringAlerts call. |

## Methods

### SearchModelMonitoringAlertsResponse

```
SearchModelMonitoringAlertsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.SearchModelMonitoringAlerts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationspecoverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationSpecOverride -->

# Class ExplanationSpecOverride (1.134.0)

`ExplanationSpecOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The ExplanationSpec entries that can be overridden at [online explanation][google.cloud.aiplatform.v1.PredictionService.Explain] time.

## Attributes |
|
|---|---|
Name |
Description |
`parameters` |
The parameters to be overridden. Note that the attribution method cannot be changed. If not specified, no parameter is overridden. |
`metadata` |
The metadata to be overridden. If not specified, no metadata is overridden. |
`examples_override` |
The example-based explanations parameter overrides. |

## Methods

### ExplanationSpecOverride

`ExplanationSpecOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The ExplanationSpec entries that can be overridden at [online explanation][google.cloud.aiplatform.v1.PredictionService.Explain] time.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespointwisemetricspec_googlecloudaiplatform_v1beta1t_6c6f79.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespointwisemetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PointwiseMetricSpec -->

# Class PointwiseMetricSpec (1.134.0)

`PointwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`metric_prompt_template` |
`str`
Required. Metric prompt template for pointwise metric. This field is a member of `oneof` _ `_metric_prompt_template` .
|

## Methods

### PointwiseMetricSpec

`PointwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesenvvar.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EnvVar -->

# Class EnvVar (1.134.0)

`EnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable present in a Container or Python Module.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name of the environment variable. Must be a valid C identifier. |
`value` |
`str`
Required. Variables that reference a $(VAR_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |

## Methods

### EnvVar

`EnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable present in a Container or Python Module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model -->

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
