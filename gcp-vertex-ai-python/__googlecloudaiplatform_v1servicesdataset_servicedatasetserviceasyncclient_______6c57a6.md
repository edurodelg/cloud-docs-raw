---
merged_at: 2026-01-25T21:47:44.360527
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicedatasetserviceasyncclient________24a342.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicedatasetserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient -->

# Class DatasetServiceAsyncClient (1.134.0)

```
DatasetServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.dataset_service.transports.base.DatasetServiceTransport,
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
google.cloud.aiplatform_v1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.dataset_service.transports.base.DatasetServiceTransport,
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
google.cloud.aiplatform_v1.types.dataset_service.CreateDatasetRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset: typing.Optional[google.cloud.aiplatform_v1.types.dataset.Dataset] = None,
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
from google.cloud import aiplatform_v1
async def sample_create_dataset():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1.[CreateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetRequest.html)(
parent="parent_value",
dataset=dataset,
)
# Make the request
operation = client.[create_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_create_dataset)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.CreateDatasetVersionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1.types.dataset_version.DatasetVersion
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
from google.cloud import aiplatform_v1
async def sample_create_dataset_version():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1.[CreateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetVersionRequest.html)(
parent="parent_value",
dataset_version=dataset_version,
)
# Make the request
operation = client.[create_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_create_dataset_version)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.DeleteDatasetRequest, dict
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
from google.cloud import aiplatform_v1
async def sample_delete_dataset():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDatasetRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_delete_dataset)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.DeleteDatasetVersionRequest,
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
from google.cloud import aiplatform_v1
async def sample_delete_dataset_version():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_delete_dataset_version)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.DeleteSavedQueryRequest,
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
from google.cloud import aiplatform_v1
async def sample_delete_saved_query():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteSavedQueryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteSavedQueryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_saved_query](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_delete_saved_query)(request=request)
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

### export_data

```
export_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.dataset_service.ExportDataRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
export_config: typing.Optional[
google.cloud.aiplatform_v1.types.dataset.ExportDataConfig
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
from google.cloud import aiplatform_v1
async def sample_export_data():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
export_config = aiplatform_v1.[ExportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataConfig.html)()
export_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1.[ExportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataRequest.html)(
name="name_value",
export_config=export_config,
)
# Make the request
operation = client.[export_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_export_data)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.GetAnnotationSpecRequest,
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
) -> google.cloud.aiplatform_v1.types.annotation_spec.AnnotationSpec
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
from google.cloud import aiplatform_v1
async def sample_get_annotation_spec():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetAnnotationSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetAnnotationSpecRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_annotation_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_get_annotation_spec)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.GetDatasetRequest, dict
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
) -> google.cloud.aiplatform_v1.types.dataset.Dataset
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
from google.cloud import aiplatform_v1
async def sample_get_dataset():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDatasetRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_get_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.GetDataset. Next ID: 4 |
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
google.cloud.aiplatform_v1.types.dataset_service.GetDatasetVersionRequest,
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
) -> google.cloud.aiplatform_v1.types.dataset_version.DatasetVersion
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
from google.cloud import aiplatform_v1
async def sample_get_dataset_version():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_get_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DatasetService.GetDatasetVersion. Next ID: 4 |
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
google.cloud.aiplatform_v1.services.dataset_service.transports.base.DatasetServiceTransport
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
google.cloud.aiplatform_v1.types.dataset_service.ImportDataRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
import_configs: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.dataset.ImportDataConfig
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
from google.cloud import aiplatform_v1
async def sample_import_data():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
import_configs = aiplatform_v1.[ImportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataConfig.html)()
import_configs.gcs_source.uris = ['uris_value1', 'uris_value2']
import_configs.import_schema_uri = "import_schema_uri_value"
request = aiplatform_v1.[ImportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataRequest.html)(
name="name_value",
import_configs=import_configs,
)
# Make the request
operation = client.[import_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_import_data)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
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
google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsAsyncPager
)
```


Lists Annotations belongs to a dataitem This RPC is only available in InternalDatasetService. It is only used for exporting conversation data to CCAI Insights.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_annotations():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_list_annotations)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest, dict
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
) -> google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_data_items():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_list_data_items)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
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
google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_dataset_versions():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDatasetVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_dataset_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_list_dataset_versions)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetsRequest, dict
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
) -> google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_datasets():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDatasetsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_datasets](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_list_datasets)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.ListSavedQueriesRequest,
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
google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_saved_queries():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSavedQueriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSavedQueriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_saved_queries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_list_saved_queries)(request=request)
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

### parse_saved_query_path

`parse_saved_query_path(path: str) -> typing.Dict[str, str]`


Parses a saved_query path into its component segments.

### restore_dataset_version

```
restore_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.dataset_service.RestoreDatasetVersionRequest,
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
from google.cloud import aiplatform_v1
async def sample_restore_dataset_version():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RestoreDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RestoreDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[restore_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_restore_dataset_version)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
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
google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_search_data_items():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsRequest.html)(
order_by_data_item="order_by_data_item_value",
dataset="dataset_value",
)
# Make the request
page_result = client.[search_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_search_data_items)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.UpdateDatasetRequest, dict
]
] = None,
*,
dataset: typing.Optional[google.cloud.aiplatform_v1.types.dataset.Dataset] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.dataset.Dataset
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
from google.cloud import aiplatform_v1
async def sample_update_dataset():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1.[UpdateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDatasetRequest.html)(
dataset=dataset,
)
# Make the request
response = await client.[update_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_update_dataset)(request=request)
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
google.cloud.aiplatform_v1.types.dataset_service.UpdateDatasetVersionRequest,
dict,
]
] = None,
*,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1.types.dataset_version.DatasetVersion
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
) -> google.cloud.aiplatform_v1.types.dataset_version.DatasetVersion
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
from google.cloud import aiplatform_v1
async def sample_update_dataset_version():
# Create a client
client = aiplatform_v1.
```[DatasetServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1.[UpdateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDatasetVersionRequest.html)(
dataset_version=dataset_version,
)
# Make the request
response = await client.[update_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient.html#google_cloud_aiplatform_v1_services_dataset_service_DatasetServiceAsyncClient_update_dataset_version)(request=request)
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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconf_0f8c0a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfi_fd9e4e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfig_0f8e4d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigs_0cdea5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigsi_f6f36b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigsim_a033e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigsimilaritysearchconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig.SimilaritySearchConfig -->

# Class SimilaritySearchConfig (1.134.0)

`SimilaritySearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to perform similarity search on memories.

## Attribute |
|
|---|---|
Name |
Description |
`embedding_model` |
`str`
Required. The model used to generate embeddings to lookup similar memories. Format: `projects/{project}/locations/{location}/publishers/google/models/{model}` .
|

## Methods

### SimilaritySearchConfig

`SimilaritySearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to perform similarity search on memories.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessupervisedtuningdatasetdistributiondatasetbucket.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningDatasetDistribution.DatasetBucket -->

# Class DatasetBucket (1.134.0)

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Attributes |
|
|---|---|
Name |
Description |
`count` |
`float`
Output only. Number of values in the bucket. |
`left` |
`float`
Output only. Left bound of the bucket. |
`right` |
`float`
Output only. Right bound of the bucket. |

## Methods

### DatasetBucket

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec -->

# Class ModelMonitoringObjectiveSpec (1.134.0)

```
ModelMonitoringObjectiveSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Monitoring objectives spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`tabular_objective` |
Tabular monitoring objective. This field is a member of `oneof` _ `objective` .
|
`explanation_spec` |
The explanation spec. This spec is required when the objectives spec includes feature attribution objectives. |
`baseline_dataset` |
Baseline dataset. It could be the training dataset or production serving dataset from a previous period. |
`target_dataset` |
Target dataset. |

## Classes

### DataDriftSpec

`DataDriftSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data drift monitoring spec. Data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.

### FeatureAttributionSpec

`FeatureAttributionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature attribution monitoring spec.

### TabularObjective

`TabularObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular monitoring objective.

## Methods

### ModelMonitoringObjectiveSpec

```
ModelMonitoringObjectiveSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Monitoring objectives spec.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresourceref_9689a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactionregionalresourcereferences.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.RegionalResourceReferences -->

# Class RegionalResourceReferences (1.134.0)

`RegionalResourceReferences(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The regional resource name or the URI. Key is region, e.g., us-central1, europe-west2, global, etc..

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`references` |
`MutableMapping[str, `
Required. |
`title` |
`str`
Required. |
`resource_title` |
`str`
Optional. Title of the resource. This field is a member of `oneof` _ `_resource_title` .
|
`resource_use_case` |
`str`
Optional. Use case (CUJ) of the resource. This field is a member of `oneof` _ `_resource_use_case` .
|
`resource_description` |
`str`
Optional. Description of the resource. This field is a member of `oneof` _ `_resource_description` .
|

## Classes

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

## Methods

### RegionalResourceReferences

`RegionalResourceReferences(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The regional resource name or the URI. Key is region, e.g., us-central1, europe-west2, global, etc..

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatereasoningenginerequest_googlecloudaipla_d623b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatereasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateReasoningEngineRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesevaluatedannotationexplanation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluatedAnnotationExplanation -->

# Class EvaluatedAnnotationExplanation (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesnotebookexecutionjobgcsnotebooksource_googleclou_028262.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnotebookexecutionjobgcsnotebooksource_googlecloud_fe0602.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnotebookexecutionjobgcsnotebooksource_googleclouda_0cff24.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookexecutionjobgcsnotebooksource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.GcsNotebookSource -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_online_serving_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service -->

# Package featurestore_online_serving_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.featurestore_online_serving_service`

package.

## Classes

[FeaturestoreOnlineServingServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceAsyncClient)

A service for serving online feature values.

[FeaturestoreOnlineServingServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceClient)

A service for serving online feature values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestooluseexample.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolUseExample -->

# Class ToolUseExample (1.134.0)

`ToolUseExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single example of the tool usage.

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
`extension_operation` |
Extension operation to call. This field is a member of `oneof` _ `Target` .
|
`function_name` |
`str`
Function name to call. This field is a member of `oneof` _ `Target` .
|
`display_name` |
`str`
Required. The display name for example. |
`query` |
`str`
Required. Query that should be routed to this tool. |
`request_params` |
`google.protobuf.struct_pb2.Struct`
Request parameters used for executing this tool. |
`response_params` |
`google.protobuf.struct_pb2.Struct`
Response parameters generated by this tool. |
`response_summary` |
`str`
Summary of the tool response to the user query. |

## Classes

### ExtensionOperation

`ExtensionOperation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Identifies one operation of the extension.

## Methods

### ToolUseExample

`ToolUseExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single example of the tool usage.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigttl_1fefec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigttlconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig.TtlConfig -->

# Class TtlConfig (1.134.0)

`TtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for automatically setting the TTL ("time-to-live") of the memories in the Memory Bank.

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
`default_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The default TTL duration of the memories in the Memory Bank. This applies to all operations that create or update a memory. This field is a member of `oneof` _ `ttl` .
|
`granular_ttl_config` |
Optional. The granular TTL configuration of the memories in the Memory Bank. This field is a member of `oneof` _ `ttl` .
|

## Classes

### GranularTtlConfig

`GranularTtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.

## Methods

### TtlConfig

`TtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for automatically setting the TTL ("time-to-live") of the memories in the Memory Bank.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstartnotebookruntimerequest_googlecloudaiplatform__c56b3c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstartnotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelevaluationsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse -->

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typeslistfeaturegroupsresponse_googlecloudaiplatform_7ad0f8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistfeaturegroupsresponse_googlecloudaiplatform__382bbb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistfeaturegroupsresponse_googlecloudaiplatform_v_68316d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistfeaturegroupsresponse_googlecloudaiplatform_v1_8739ec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeaturegroupsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelgardensource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelGardenSource -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratefetchaccesstokenresponse_googleclouda_8ea2a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratefetchaccesstokenresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenResponse -->

# Class GenerateFetchAccessTokenResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatemodeldeploymentmonitoringjoboperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelDeploymentMonitoringJobOperationMetadata -->

# Class UpdateModelDeploymentMonitoringJobOperationMetadata (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetannotationspecrequest_googlecloudaiplatfo_5ef148.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetannotationspecrequest_googlecloudaiplatfor_02c966.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetannotationspecrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrebootpersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatetrainingpipelinerequest_googlecloudaipl_d9ec86.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatetrainingpipelinerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest -->

# Class CreateTrainingPipelineRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescancelhyperparametertuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelHyperparameterTuningJobRequest -->

# Class CancelHyperparameterTuningJobRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdateexplanationdatasetrequest_googlecloud_eacde9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdateexplanationdatasetrequest_googleclouda_ec5120.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdateexplanationdatasetrequest_googlecloudai_a8b5d8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateexplanationdatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest -->

# Class UpdateExplanationDatasetRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnotebookruntimesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesevaluatedannotationexplanation_googlecloudaip_8ded9f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluatedannotationexplanation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotationExplanation -->

# Class EvaluatedAnnotationExplanation (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvertexaisearchconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAiSearchConfig -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdateexamplestorerequest_googlecloudaiplatf_3888c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdateexamplestorerequest_googlecloudaiplatfo_e28f86.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateexamplestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatebatchpredictionjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateBatchPredictionJobRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesprobegrpcaction_googlecloudaiplatform_v1beta1types_dc3dbb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprobegrpcaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe.GrpcAction -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatebatchpredictionjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateBatchPredictionJobRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesextension_registry_serviceextensionregistryserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient -->

# Class ExtensionRegistryServiceAsyncClient (1.134.0)

```
ExtensionRegistryServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### ExtensionRegistryServiceAsyncClient

```
ExtensionRegistryServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the extension registry service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ExtensionRegistryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_delete_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExtensionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceAsyncClient_delete_extension)(request=request)
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
The request object. Request message for ExtensionRegistryService.DeleteExtension. |
`name` |
Required. The name of the Extension resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ExtensionRegistryServiceAsyncClient` |
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
`ExtensionRegistryServiceAsyncClient` |
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
`ExtensionRegistryServiceAsyncClient` |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_get_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetExtensionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExtensionRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceAsyncClient_get_extension)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExtensionRegistryService.GetExtension. |
`name` |
Required. The name of the Extension resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.services.extension_registry_service.transports.base.ExtensionRegistryServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
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
async def sample_import_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html)()
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
operation = client.[import_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceAsyncClient_import_extension)(request=request)
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
The request object. Request message for ExtensionRegistryService.ImportExtension. |
`parent` |
Required. The resource name of the Location to import the Extension in. Format: |
`extension` |
Required. The Extension to import. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsAsyncPager
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
async def sample_list_extensions():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListExtensionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_extensions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceAsyncClient_list_extensions)(request=request)
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
The request object. Request message for ExtensionRegistryService.ListExtensions. |
`parent` |
Required. The resource name of the Location to list the Extensions from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_update_extension():
# Create a client
client = aiplatform_v1beta1.
```[ExtensionRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html)()
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
response = await client.[update_extension](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_extension_registry_service_ExtensionRegistryServiceAsyncClient_update_extension)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExtensionRegistryService.UpdateExtension. |
`extension` |
Required. The Extension which replaces the resource on the server. This corresponds to the |
`update_mask` |
Required. Mask specifying which fields to update. Supported fields: :: * |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinp_fae238.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinpu_ab7d9f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinput_a314f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputs_7318eb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputst_324611.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstr_5b4162.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstra_3ee0c2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformationautotransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetpersistentresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPersistentResourceRequest -->

# Class GetPersistentResourceRequest (1.134.0)

```
GetPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.GetPersistentResource.

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

### GetPersistentResourceRequest

```
GetPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.GetPersistentResource.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextsentiment_g_576094.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextsentiment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentiment -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateexplanationdatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetRequest -->

# Class UpdateExplanationDatasetRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespartialarg__googlecloudaiplatform_v1servicesendpoi_8c32a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespartialarg.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PartialArg -->

# Class PartialArg (1.134.0)

`PartialArg(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Partial argument value of the function call.

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
`null_value` |
`google.protobuf.struct_pb2.NullValue`
Optional. Represents a null value. This field is a member of `oneof` _ `delta` .
|
`number_value` |
`float`
Optional. Represents a double value. This field is a member of `oneof` _ `delta` .
|
`string_value` |
`str`
Optional. Represents a string value. This field is a member of `oneof` _ `delta` .
|
`bool_value` |
`bool`
Optional. Represents a boolean value. This field is a member of `oneof` _ `delta` .
|
`json_path` |
`str`
Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. "$.foo.bar[0].data". |
`will_continue` |
`bool`
Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow. |

## Methods

### PartialArg

`PartialArg(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Partial argument value of the function call.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesendpoint_service_googlecloudaiplatform_v1typesl_5f279a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesendpoint_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistbatchpredictionjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdatemodeldeploymentmonitoringjoboperation_15d392.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatemodeldeploymentmonitoringjoboperationm_2485ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatemodeldeploymentmonitoringjoboperationme_a6f9d4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatemodeldeploymentmonitoringjoboperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobOperationMetadata -->

# Class UpdateModelDeploymentMonitoringJobOperationMetadata (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportpublishermodelresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelResponse -->

# Class ExportPublisherModelResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespoststartupscriptconfigpoststartupscriptbehavior_g_049fb2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespoststartupscriptconfigpoststartupscriptbehavior.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PostStartupScriptConfig.PostStartupScriptBehavior -->

# Class PostStartupScriptBehavior (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespairwisequestionansweringqualityspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualitySpec -->

# Class PairwiseQuestionAnsweringQualitySpec (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadatainputmetadatafeaturevaluedomain_cb9186.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadatafeaturevaluedomain.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.FeatureValueDomain -->

# Class FeatureValueDomain (1.134.0)

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

## Attributes |
|
|---|---|
Name |
Description |
`min_value` |
`float`
The minimum permissible value for this feature. |
`max_value` |
`float`
The maximum permissible value for this feature. |
`original_mean` |
`float`
If this input feature has been normalized to a mean value of 0, the original_mean specifies the mean value of the domain prior to normalization. |
`original_stddev` |
`float`
If this input feature has been normalized to a standard deviation of 1.0, the original_stddev specifies the standard deviation of the domain prior to normalization. |

## Methods

### FeatureValueDomain

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesassignnotebookruntimeoperationmetadata_googlecloud_f2efe0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesassignnotebookruntimeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AssignNotebookRuntimeOperationMetadata -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamRawPredictRequest -->

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typessetpublishermodelconfigrequest_googlecloud_9dfb49.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessetpublishermodelconfigrequest_googleclouda_f225c8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessetpublishermodelconfigrequest_googlecloudai_542a74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessetpublishermodelconfigrequest_googlecloudaip_e759c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessetpublishermodelconfigrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescitation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Citation -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslisttensorboardrunsresponse_googlecloudaiplatform__20579d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttensorboardrunsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrialstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial.State -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeletefeaturevaluesrequestselectentity_googleclou_c9e097.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletefeaturevaluesrequestselectentity_googlecloud_84b13a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturevaluesrequestselectentity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest.SelectEntity -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassembledatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmodelmonitoringjobsresponse_googlecloudai_83fbcd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelmonitoringjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse -->

# Class ListModelMonitoringJobsResponse (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstartnotebookruntimeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeOperationMetadata -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessuggesttrialsresponse_googlecloudaiplatform_7e31c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessuggesttrialsresponse_googlecloudaiplatform__690efb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessuggesttrialsresponse_googlecloudaiplatform_v_a0f8a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessuggesttrialsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgettensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardTimeSeriesRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistreasoningenginesresponse_googlecloudaiplatform_a558bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistreasoningenginesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetdatasetversionrequest_googlecloudaiplatfo_585078.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetdatasetversionrequest_googlecloudaiplatfor_0467b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetdatasetversionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetVersionRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateendpointoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointOperationMetadata -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewdirectwriterequestdatakeyandfeatur_450dba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewdirectwriterequestdatakeyandfeaturevaluesfeaturefeaturevalueandtimestamp.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues.Feature.FeatureValueAndTimestamp -->

# Class FeatureValueAndTimestamp (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistoptimaltrialsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint -->

# Class Endpoint (1.134.0)

```
Endpoint(
endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an endpoint resource.

## Parameters |
|
|---|---|
Name |
Description |
`endpoint_name` |
`str`
Required. A fully-qualified endpoint resource name or endpoint ID. Example: "projects/123/locations/us-central1/endpoints/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve endpoint from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

## Properties

### create_time

Time this resource was created.

### dedicated_endpoint_dns

The dedicated endpoint dns for this Endpoint.

This property is only available if dedicated endpoint is enabled. If dedicated endpoint is not enabled, this property returns None.

### dedicated_endpoint_enabled

The dedicated endpoint is enabled for this Endpoint.

This property will be true if dedicated endpoint is enabled.

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

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
Endpoint should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

### preview

Return an Endpoint instance with preview features enabled.

### private_service_connect_config

The Private Service Connect configuration for this Endpoint.

### resource_name

Full qualified resource name.

### traffic_split

A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's ID is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

### update_time

Time this resource was last updated.

## Methods

### create

```
create(
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync=True,
create_request_timeout: typing.Optional[float] = None,
endpoint_id: typing.Optional[str] = None,
enable_request_response_logging=False,
request_response_logging_sampling_rate: typing.Optional[float] = None,
request_response_logging_bq_destination_table: typing.Optional[str] = None,
dedicated_endpoint_enabled=False,
inference_timeout: typing.Optional[int] = None,
) -> google.cloud.aiplatform.models.Endpoint
```


Creates a new endpoint.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Endpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the Endpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`project` |
`str`
Optional. Project to retrieve endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve endpoint from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`endpoint_id` |
`str`
Optional. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. This value should be 1-10 characters, and valid characters are /[0-9]/. When using HTTP/JSON, this field is populated based on a query string argument, such as |
`request_response_logging_sampling_rate` |
`float`
Optional. The request response logging sampling rate. If not set, default is 0.0. |
`request_response_logging_bq_destination_table` |
`str`
Optional. The request response logging bigquery destination. If not set, will create a table with name: |
`inference_timeout` |
`int`
Optional. It defines the prediction timeout, in seconds, for online predictions using cloud-based endpoints. This applies to either PSC endpoints, when private_service_connect_config is set, or dedicated endpoints, when dedicated_endpoint_enabled is true. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_request_response_logging` |
`bool`
Optional. Whether to enable request & response logging for this endpoint. |
`dedicated_endpoint_enabled` |
`bool`
Optional. If enabled, a dedicated dns will be created and your traffic will be fully isolated from other customers' traffic and latency will be reduced. |

Returns |
|
|---|---|
Type |
Description |
`endpoint (aiplatform.Endpoint)` |
Created endpoint. |

### delete

`delete(force: bool = False, sync: bool = True) -> None`


Deletes this Vertex AI Endpoint resource. If force is set to True, all models on this Endpoint will be undeployed prior to deletion.

Parameters |
|
|---|---|
Name |
Description |
`force` |
`bool`
Required. If force is set to True, all deployed models on this Endpoint will be undeployed first. Default is False. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`FailedPrecondition` |
If models are deployed on this Endpoint and force = False. |

### deploy

```
deploy(
model: google.cloud.aiplatform.models.Model,
deployed_model_display_name: typing.Optional[str] = None,
traffic_percentage: int = 0,
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
) -> None
```


Deploys a Model to the Endpoint.

Parameters |
|
|---|---|
Name |
Description |
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
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the larger value of min_replica_count or 1 will be used. If value provided is smaller than min_replica_count, it will automatically be increased to be min_replica_count. |
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
Optional. The TPU topology to use for the DeployedModel. Required for CloudTPU multihost deployments. |
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
`model` |
`aiplatform.Model`
Required. Model to be deployed. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_access_logging` |
`bool`
Whether to enable endpoint access logging. Defaults to False. |

### direct_predict

```
direct_predict(
inputs: typing.List,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction against this Endpoint for a pre-built image.

Parameters |
|
|---|---|
Name |
Description |
`inputs` |
`List`
Required. The inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_predict_async

```
direct_predict_async(
inputs: typing.List,
*,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes an asynchronous direct (gRPC) prediction against this Endpoint for a pre-built image.

Example usage:

```
response = await my_endpoint.direct_predict_async(inputs=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`inputs` |
`List`
Required. The inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_raw_predict

```
direct_raw_predict(
method_name: str, request: bytes, timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction request using arbitrary headers for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
response = my_endpoint.direct_raw_predict(request=b'...')
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`request` |
`bytes`
The body of the prediction request in bytes. |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_raw_predict_async

```
direct_raw_predict_async(
method_name: str, request: bytes, timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction request for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
response = await my_endpoint.direct_raw_predict(request=b'...')
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`request` |
`bytes`
The body of the prediction request in bytes. |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### explain

```
explain(
instances: typing.List[typing.Dict],
parameters: typing.Optional[typing.Dict] = None,
deployed_model_id: typing.Optional[str] = None,
timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction with explanations against this Endpoint.

Example usage: response = my_endpoint.explain(instances=[...]) my_explanations = response.explanations

Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`deployed_model_id` |
`str`
Optional. If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions, explanations, and Model ID. |

### explain_async

```
explain_async(
instances: typing.List[typing.Dict],
*,
parameters: typing.Optional[typing.Dict] = None,
deployed_model_id: typing.Optional[str] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction with explanations against this Endpoint.

Example usage:

```
response = await my_endpoint.explain_async(instances=[...])
my_explanations = response.explanations
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`deployed_model_id` |
`str`
Optional. If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions, explanations, and Model ID. |

### invoke

```
invoke(
request_path: str,
body: bytes,
headers: typing.Dict[str, str],
deployed_model_id: typing.Optional[str] = None,
stream: bool = False,
timeout: typing.Optional[float] = None,
) -> typing.Union[requests.models.Response, typing.Iterator[requests.models.Response]]
```


Makes a prediction request for arbitrary paths.

Example usage: my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)

# Unary request

```
body = {
"model": "",
"messages": [
{
"role": "user",
"content": "Hello!",
}
],
}
response = my_endpoint.invoke(
request_path="/v1/chat/completions",
body = json.dumps(body).encode("utf-8"),
headers = {'Content-Type':'application/json'},
)
status_code = response.status_code
results = json.dumps(response.text)
# Streaming request
body = {
"model": "",
"messages": [
{
"role": "user",
"content": "Hello!",
}
],
"stream": "true",
}
for chunk in my_endpoint.invoke(
request_path="/v1/chat/completions",
body = json.dumps(body).encode("utf-8"),
headers = {'Content-Type':'application/json'},
stream=True,
):
chunk_text = chunk.decode('utf-8')
```


Parameters |
|
|---|---|
Name |
Description |
`request_path` |
`str`
The request url to the model server. The request path must be a string that starts with a forward slash. Root can't be accessed. |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 1.5 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`deployed_model_id` |
`str`
Optional. If specified, this InvokeRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`stream` |
`bool`
If set to True, streaming will be enabled. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ImportError` |
If there is an issue importing the `TCPKeepAliveAdapter` package. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.models.Endpoint]
```


List all Endpoint resource instances.

Example Usage: aiplatform.Endpoint.list( filter='labels.my_label="my_label_value" OR display_name=!"old_endpoint"', )

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
`List[models.Endpoint]` |
A list of Endpoint resource objects |

### list_models

```
list_models() -> (
typing.List[google.cloud.aiplatform_v1.types.endpoint.DeployedModel]
)
```


Returns a list of the models deployed to this Endpoint.

Returns |
|
|---|---|
Type |
Description |
`deployed_models (List[aiplatform.gapic.DeployedModel])` |
A list of the models deployed in this Endpoint. |

### predict

```
predict(
instances: typing.List,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
use_raw_predict: typing.Optional[bool] = False,
*,
use_dedicated_endpoint: typing.Optional[bool] = False
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction against this Endpoint.

Example usage:

```
response = my_endpoint.predict(instances=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |
`use_raw_predict` |
`bool`
Optional. Default value is False. If set to True, the underlying prediction call will be made against Endpoint.raw_predict(). |
`use_dedicated_endpoint` |
`bool`
Optional. Default value is False. If set to True, the underlying prediction call will be made using the dedicated endpoint dns. |

Exceptions |
|
|---|---|
Type |
Description |
`ImportError` |
If there is an issue importing the `TCPKeepAliveAdapter` package. |
`ValueError` |
If the dedicated endpoint DNS is empty for dedicated endpoints. |
`ValueError` |
If the prediction request fails for dedicated endpoints. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions and Model ID. |

### predict_async

```
predict_async(
instances: typing.List,
*,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Make an asynchronous prediction against this Endpoint. Example usage:

```
response = await my_endpoint.predict_async(instances=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions and Model ID. |

### raw_predict

```
raw_predict(
body: bytes,
headers: typing.Dict[str, str],
*,
use_dedicated_endpoint: typing.Optional[bool] = False,
timeout: typing.Optional[float] = None
) -> requests.models.Response
```


Makes a prediction request using arbitrary headers.

Example usage: my_endpoint = aiplatform.Endpoint(ENDPOINT_ID) response = my_endpoint.raw_predict( body = b'{"instances":[{"feat_1":val_1, "feat_2":val_2}]}' headers = {'Content-Type':'application/json'} ) status_code = response.status_code results = json.dumps(response.text)

Parameters |
|
|---|---|
Name |
Description |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 1.5 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`use_dedicated_endpoint` |
`bool`
Optional. Default value is False. If set to True, the underlying prediction call will be made using the dedicated endpoint dns. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ImportError` |
If there is an issue importing the `TCPKeepAliveAdapter` package. |

### stream_direct_predict

```
stream_direct_predict(
inputs_iterator: typing.Iterator[typing.List],
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
) -> typing.Iterator[google.cloud.aiplatform.models.Prediction]
```


Makes a streaming direct (gRPC) prediction against this Endpoint for a pre-built image.

Parameters |
|
|---|---|
Name |
Description |
`inputs_iterator` |
`Iterator[List]`
Required. An iterator of the inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float] :Yields: *predictions (Iterator[aiplatform.Prediction])* -- The resulting streamed predictions.`
Optional. The timeout for this request in seconds. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
method_name: str,
requests: typing.Iterator[bytes],
timeout: typing.Optional[float] = None,
) -> typing.Iterator[google.cloud.aiplatform.models.Prediction]
```


Makes a direct (gRPC) streaming prediction request for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
for stream_response in my_endpoint.stream_direct_raw_predict(
request=b'...'
):
yield stream_response
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`requests` |
`Iterator[bytes]`
The body of the prediction requests in bytes. |
`timeout` |
`Optional[float] :Yields: *predictions (Iterator[aiplatform.Prediction])* -- The resulting streamed predictions.`
Optional. The timeout for this request in seconds. |

### stream_raw_predict

```
stream_raw_predict(
body: bytes,
headers: typing.Dict[str, str],
*,
use_dedicated_endpoint: typing.Optional[bool] = False,
timeout: typing.Optional[float] = None
) -> typing.Iterator[requests.models.Response]
```


Makes a streaming prediction request using arbitrary headers. For custom model, this method is only supported for dedicated endpoint.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
for stream_response in my_endpoint.stream_raw_predict(
body = b'{"instances":[{"feat_1":val_1, "feat_2":val_2}]}'
headers = {'Content-Type':'application/json'}
):
status_code = response.status_code
stream_result = json.dumps(response.text)
```
```


Parameters |
|
|---|---|
Name |
Description |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 10 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`use_dedicated_endpoint` |
`bool`
Optional. Default value is False. If set to True, the underlying prediction call will be made using the dedicated endpoint dns. |
`timeout` |
`float :Yields: *predictions (Iterator[requests.models.Response])* -- The streaming prediction results.`
Optional. The timeout for this request in seconds. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### undeploy

```
undeploy(
deployed_model_id: str,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync=True,
) -> None
```


Undeploys a deployed model.

The model to be undeployed should have no traffic or user must provide
a new traffic_split with the remaining deployed models. Refer
to `Endpoint.traffic_split`

for the current traffic split mapping.

Parameters |
|
|---|---|
Name |
Description |
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the Endpoint. |
`traffic_split` |
`Dict[str, int]`
Optional. A map of DeployedModel IDs to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. Required if undeploying a model with non-zero traffic from an Endpoint with multiple deployed models. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. If a DeployedModel's ID is not listed in this map, then it receives no traffic. |
`metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |

### undeploy_all

`undeploy_all(sync: bool = True) -> google.cloud.aiplatform.models.Endpoint`


Undeploys every model deployed to this Endpoint.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### update

```
update(
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Endpoint
```


Updates an endpoint.

Example usage: my_endpoint = my_endpoint.update( display_name='my-updated-endpoint', description='my updated description', labels={'key': 'value'}, traffic_split={ '123456': 20, '234567': 80, }, )

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The display name of the Endpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the Endpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`traffic_split` |
`Dict[str, int]`
Optional. A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

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
`Endpoint (aiplatform.Prediction)` |
Updated endpoint resource. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicemodelserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient -->

# Class ModelServiceAsyncClient (1.134.0)

```
ModelServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.model_service.transports.base.ModelServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.model_service.transports.base.ModelServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning Models.

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
`ModelServiceTransport` |
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

### ModelServiceAsyncClient

```
ModelServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.model_service.transports.base.ModelServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.model_service.transports.base.ModelServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ModelServiceTransport,Callable[..., ModelServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_import_evaluated_annotations

```
batch_import_evaluated_annotations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.BatchImportEvaluatedAnnotationsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
evaluated_annotations: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.evaluated_annotation.EvaluatedAnnotation
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
) -> (
google.cloud.aiplatform_v1.types.model_service.BatchImportEvaluatedAnnotationsResponse
)
```


Imports a list of externally generated EvaluatedAnnotations.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_batch_import_evaluated_annotations():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchImportEvaluatedAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportEvaluatedAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[batch_import_evaluated_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_batch_import_evaluated_annotations)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.BatchImportEvaluatedAnnotations |
`parent` |
Required. The name of the parent ModelEvaluationSlice resource. Format: |
`evaluated_annotations` |
`:class:`
Required. Evaluated annotations resource to be imported. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.BatchImportEvaluatedAnnotations |

### batch_import_model_evaluation_slices

```
batch_import_model_evaluation_slices(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.BatchImportModelEvaluationSlicesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_evaluation_slices: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.model_evaluation_slice.ModelEvaluationSlice
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
) -> (
google.cloud.aiplatform_v1.types.model_service.BatchImportModelEvaluationSlicesResponse
)
```


Imports a list of externally generated ModelEvaluationSlice.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_batch_import_model_evaluation_slices():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchImportModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[batch_import_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_batch_import_model_evaluation_slices)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.BatchImportModelEvaluationSlices |
`parent` |
Required. The name of the parent ModelEvaluation resource. Format: |
`model_evaluation_slices` |
`:class:`
Required. Model evaluation slice resource to be imported. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.BatchImportModelEvaluationSlices |

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

### copy_model

```
copy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.CopyModelRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
source_model: typing.Optional[str] = None,
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


Copies an already existing Vertex AI Model into the specified Location. The source Model must exist in the same Project. When copying custom Models, the users themselves are responsible for xref_Model.metadata content to be region-agnostic, as well as making sure that any resources (e.g. files) it depends on remain accessible.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_copy_model():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CopyModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CopyModelRequest.html)(
model_id="model_id_value",
parent="parent_value",
source_model="source_model_value",
)
# Make the request
operation = client.[copy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_copy_model)(request=request)
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
The request object. Request message for ModelService.CopyModel. |
`parent` |
Required. The resource name of the Location into which to copy the Model. Format: |
`source_model` |
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_model

```
delete_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.DeleteModelRequest, dict
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


Deletes a Model.

A model cannot be deleted if any xref_Endpoint resource has a xref_DeployedModel based on the model in its xref_deployed_models field.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_model():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_delete_model)(request=request)
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
The request object. Request message for ModelService.DeleteModel. |
`name` |
Required. The name of the Model resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_model_version

```
delete_model_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.DeleteModelVersionRequest,
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


Deletes a Model version.

Model version can only be deleted if there are no xref_DeployedModels created from it. Deleting the only version in the Model is not allowed. Use xref_DeleteModel for deleting the Model instead.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_model_version():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteModelVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteModelVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_delete_model_version)(request=request)
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
The request object. Request message for ModelService.DeleteModelVersion. |
`name` |
Required. The name of the model version to be deleted, with a version ID explicitly included. Example: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### export_model

```
export_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ExportModelRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
output_config: typing.Optional[
google.cloud.aiplatform_v1.types.model_service.ExportModelRequest.OutputConfig
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


Exports a trained, exportable Model to a location specified by the user. A Model is considered to be exportable if it has at least one [supported export format][google.cloud.aiplatform.v1.Model.supported_export_formats].

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_export_model():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ExportModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[export_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_export_model)(request=request)
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
The request object. Request message for ModelService.ExportModel. |
`name` |
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. This corresponds to the |
`output_config` |
Required. The desired output location and configuration. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ModelServiceAsyncClient` |
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
`ModelServiceAsyncClient` |
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
`ModelServiceAsyncClient` |
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

### get_model

```
get_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.GetModelRequest, dict
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
) -> google.cloud.aiplatform_v1.types.model.Model
```


Gets a Model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_model():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_get_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.GetModel. |
`name` |
Required. The name of the Model resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A trained machine learning Model. |

### get_model_evaluation

```
get_model_evaluation(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.GetModelEvaluationRequest,
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
) -> google.cloud.aiplatform_v1.types.model_evaluation.ModelEvaluation
```


Gets a ModelEvaluation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_model_evaluation():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelEvaluationRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_get_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.GetModelEvaluation. |
`name` |
Required. The name of the ModelEvaluation resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data. |

### get_model_evaluation_slice

```
get_model_evaluation_slice(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.GetModelEvaluationSliceRequest,
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
) -> google.cloud.aiplatform_v1.types.model_evaluation_slice.ModelEvaluationSlice
```


Gets a ModelEvaluationSlice.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_model_evaluation_slice():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetModelEvaluationSliceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelEvaluationSliceRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_model_evaluation_slice](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_get_model_evaluation_slice)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.GetModelEvaluationSlice. |
`name` |
Required. The name of the ModelEvaluationSlice resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations. |

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
google.cloud.aiplatform_v1.services.model_service.transports.base.ModelServiceTransport
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

### import_model_evaluation

```
import_model_evaluation(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ImportModelEvaluationRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_evaluation: typing.Optional[
google.cloud.aiplatform_v1.types.model_evaluation.ModelEvaluation
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.model_evaluation.ModelEvaluation
```


Imports an externally generated ModelEvaluation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_import_model_evaluation():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ImportModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportModelEvaluationRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[import_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_import_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.ImportModelEvaluation |
`parent` |
Required. The name of the parent model resource. Format: |
`model_evaluation` |
Required. Model evaluation resource to be imported. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data. |

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

### list_model_evaluation_slices

```
list_model_evaluation_slices(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
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
google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationSlicesAsyncPager
)
```


Lists ModelEvaluationSlices in a ModelEvaluation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_model_evaluation_slices():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_list_model_evaluation_slices)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluationSlices. |
`parent` |
Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.ListModelEvaluationSlices. Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_evaluations

```
list_model_evaluations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
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
google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationsAsyncPager
)
```


Lists ModelEvaluations in a Model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_model_evaluations():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListModelEvaluationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_list_model_evaluations)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluations. |
`parent` |
Required. The resource name of the Model to list the ModelEvaluations from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.ListModelEvaluations. Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_version_checkpoints

```
list_model_version_checkpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
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
google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionCheckpointsAsyncPager
)
```


Lists checkpoints of the specified model version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_model_version_checkpoints():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListModelVersionCheckpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_version_checkpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_list_model_version_checkpoints)(request=request)
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
The request object. Request message for ModelService.ListModelVersionCheckpoints. |
`name` |
Required. The name of the model version to list checkpoints for. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.ListModelVersionCheckpoints Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_versions

```
list_model_versions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
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
google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionsAsyncPager
)
```


Lists versions of the specified model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_model_versions():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListModelVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_list_model_versions)(request=request)
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
The request object. Request message for ModelService.ListModelVersions. |
`name` |
Required. The name of the model to list versions for. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.ListModelVersions Iterating over this object will yield results and resolve additional pages automatically. |

### list_models

```
list_models(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.ListModelsRequest, dict
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
) -> google.cloud.aiplatform_v1.services.model_service.pagers.ListModelsAsyncPager
```


Lists Models in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_models():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_list_models)(request=request)
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
The request object. Request message for ModelService.ListModels. |
`parent` |
Required. The resource name of the Location to list the Models from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.ListModels Iterating over this object will yield results and resolve additional pages automatically. |

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

### merge_version_aliases

```
merge_version_aliases(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.MergeVersionAliasesRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
version_aliases: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.model.Model
```


Merges a set of aliases for a Model version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_merge_version_aliases():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[MergeVersionAliasesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MergeVersionAliasesRequest.html)(
name="name_value",
version_aliases=['version_aliases_value1', 'version_aliases_value2'],
)
# Make the request
response = await client.[merge_version_aliases](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_merge_version_aliases)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.MergeVersionAliases. |
`name` |
Required. The name of the model version to merge aliases, with a version ID explicitly included. Example: |
`version_aliases` |
`:class:`
Required. The set of version aliases to merge. The alias should be at most 128 characters, and match |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A trained machine learning Model. |

### model_evaluation_path

```
model_evaluation_path(
project: str, location: str, model: str, evaluation: str
) -> str
```


Returns a fully-qualified model_evaluation string.

### model_evaluation_slice_path

```
model_evaluation_slice_path(
project: str, location: str, model: str, evaluation: str, slice: str
) -> str
```


Returns a fully-qualified model_evaluation_slice string.

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

### parse_model_evaluation_path

`parse_model_evaluation_path(path: str) -> typing.Dict[str, str]`


Parses a model_evaluation path into its component segments.

### parse_model_evaluation_slice_path

`parse_model_evaluation_slice_path(path: str) -> typing.Dict[str, str]`


Parses a model_evaluation_slice path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

### update_explanation_dataset

```
update_explanation_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.UpdateExplanationDatasetRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
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


Incrementally update the dataset used for an examples model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_explanation_dataset():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateExplanationDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetRequest.html)(
model="model_value",
)
# Make the request
operation = client.[update_explanation_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_update_explanation_dataset)(request=request)
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
The request object. Request message for ModelService.UpdateExplanationDataset. |
`model` |
Required. The resource name of the Model to update. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### update_model

```
update_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.UpdateModelRequest, dict
]
] = None,
*,
model: typing.Optional[google.cloud.aiplatform_v1.types.model.Model] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.model.Model
```


Updates a Model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_model():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
model = aiplatform_v1.Model()
model.display_name = "display_name_value"
request = aiplatform_v1.[UpdateModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelRequest.html)(
model=model,
)
# Make the request
response = await client.[update_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_update_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.UpdateModel. |
`model` |
Required. The Model which replaces the resource on the server. When Model Versioning is enabled, the model.name will be used to determine whether to update the model or model version. 1. model.name with the @ value, e.g. models/123@1, refers to a version specific update. 2. model.name without the @ value, e.g. models/123, refers to a model update. 3. model.name with @-, e.g. models/123@-, refers to a model update. 4. Supported model fields: display_name, description; supported version-specific fields: version_description. Labels are supported in both scenarios. Both the model labels and the version labels are merged when a model is returned. When updating labels, if the request is for model-specific update, model label gets updated. Otherwise, version labels get updated. 5. A model name or model version name fields update mismatch will cause a precondition error. 6. One request cannot update both the model and the version fields. You must update them separately. This corresponds to the |
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
A trained machine learning Model. |

### upload_model

```
upload_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.model_service.UploadModelRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[google.cloud.aiplatform_v1.types.model.Model] = None,
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


Uploads a Model artifact into Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_upload_model():
# Create a client
client = aiplatform_v1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
model = aiplatform_v1.Model()
model.display_name = "display_name_value"
request = aiplatform_v1.[UploadModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadModelRequest.html)(
parent="parent_value",
model=model,
)
# Make the request
operation = client.[upload_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1_services_model_service_ModelServiceAsyncClient_upload_model)(request=request)
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
The request object. Request message for ModelService.UploadModel. |
`parent` |
Required. The resource name of the Location into which to upload the Model. Format: |
`model` |
Required. The Model to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
