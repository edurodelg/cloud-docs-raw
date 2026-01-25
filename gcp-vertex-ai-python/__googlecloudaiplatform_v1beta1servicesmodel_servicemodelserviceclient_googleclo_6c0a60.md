---
merged_at: 2026-01-25T21:47:44.363192
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicemodelserviceclient_googleclou_a93b9a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicemodelserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient -->

# Class ModelServiceClient (1.134.0)

```
ModelServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### ModelServiceClient

```
ModelServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_import_evaluated_annotations

```
batch_import_evaluated_annotations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportEvaluatedAnnotationsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
evaluated_annotations: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.evaluated_annotation.EvaluatedAnnotation
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
) -> (
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportEvaluatedAnnotationsResponse
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
from google.cloud import aiplatform_v1beta1
def sample_batch_import_evaluated_annotations():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchImportEvaluatedAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[batch_import_evaluated_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_batch_import_evaluated_annotations)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.BatchImportEvaluatedAnnotations |
`parent` |
`str`
Required. The name of the parent ModelEvaluationSlice resource. Format: |
`evaluated_annotations` |
`MutableSequence[`
Required. Evaluated annotations resource to be imported. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportModelEvaluationSlicesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_evaluation_slices: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.model_evaluation_slice.ModelEvaluationSlice
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
) -> (
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportModelEvaluationSlicesResponse
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
from google.cloud import aiplatform_v1beta1
def sample_batch_import_model_evaluation_slices():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchImportModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[batch_import_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_batch_import_model_evaluation_slices)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.BatchImportModelEvaluationSlices |
`parent` |
`str`
Required. The name of the parent ModelEvaluation resource. Format: |
`model_evaluation_slices` |
`MutableSequence[`
Required. Model evaluation slice resource to be imported. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### copy_model

```
copy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.CopyModelRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
source_model: typing.Optional[str] = None,
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


Copies an already existing Vertex AI Model into the specified Location. The source Model must exist in the same Project. When copying custom Models, the users themselves are responsible for xref_Model.metadata content to be region-agnostic, as well as making sure that any resources (e.g. files) it depends on remain accessible.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_copy_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CopyModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest.html)(
model_id="model_id_value",
parent="parent_value",
source_model="source_model_value",
)
# Make the request
operation = client.[copy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_copy_model)(request=request)
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
The request object. Request message for ModelService.CopyModel. |
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: |
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_model

```
delete_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.DeleteModelRequest, dict
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
from google.cloud import aiplatform_v1beta1
def sample_delete_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_delete_model)(request=request)
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
The request object. Request message for ModelService.DeleteModel. |
`name` |
`str`
Required. The name of the Model resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_model_version

```
delete_model_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.DeleteModelVersionRequest,
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
from google.cloud import aiplatform_v1beta1
def sample_delete_model_version():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_delete_model_version)(request=request)
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
The request object. Request message for ModelService.DeleteModelVersion. |
`name` |
`str`
Required. The name of the model version to be deleted, with a version ID explicitly included. Example: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### export_model

```
export_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ExportModelRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
output_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_service.ExportModelRequest.OutputConfig
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


Exports a trained, exportable Model to a location specified by the user. A Model is considered to be exportable if it has at least one [supported export format][google.cloud.aiplatform.v1beta1.Model.supported_export_formats].

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_export_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ExportModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[export_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_export_model)(request=request)
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
The request object. Request message for ModelService.ExportModel. |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. This corresponds to the |
`output_config` |
Required. The desired output location and configuration. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`ModelServiceClient` |
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
`ModelServiceClient` |
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
`ModelServiceClient` |
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

### get_model

```
get_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.GetModelRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.types.model.Model
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
from google.cloud import aiplatform_v1beta1
def sample_get_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_get_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.GetModel. |
`name` |
`str`
Required. The name of the Model resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.GetModelEvaluationRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.model_evaluation.ModelEvaluation
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
from google.cloud import aiplatform_v1beta1
def sample_get_model_evaluation():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_get_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.GetModelEvaluation. |
`name` |
`str`
Required. The name of the ModelEvaluation resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.GetModelEvaluationSliceRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.model_evaluation_slice.ModelEvaluationSlice
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
from google.cloud import aiplatform_v1beta1
def sample_get_model_evaluation_slice():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelEvaluationSliceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationSliceRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_evaluation_slice](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_get_model_evaluation_slice)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.GetModelEvaluationSlice. |
`name` |
`str`
Required. The name of the ModelEvaluationSlice resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### import_model_evaluation

```
import_model_evaluation(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ImportModelEvaluationRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_evaluation: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_evaluation.ModelEvaluation
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model_evaluation.ModelEvaluation
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
from google.cloud import aiplatform_v1beta1
def sample_import_model_evaluation():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ImportModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportModelEvaluationRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[import_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_import_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.ImportModelEvaluation |
`parent` |
`str`
Required. The name of the parent model resource. Format: |
`model_evaluation` |
Required. Model evaluation resource to be imported. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### list_model_evaluation_slices

```
list_model_evaluation_slices(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesRequest,
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
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationSlicesPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_model_evaluation_slices():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_evaluation_slices)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluationSlices. |
`parent` |
`str`
Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
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
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_model_evaluations():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelEvaluationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_evaluations)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluations. |
`parent` |
`str`
Required. The resource name of the Model to list the ModelEvaluations from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
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
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionCheckpointsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_model_version_checkpoints():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelVersionCheckpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_version_checkpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_version_checkpoints)(request=request)
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
The request object. Request message for ModelService.ListModelVersionCheckpoints. |
`name` |
`str`
Required. The name of the model version to list checkpoints for. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
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
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_model_versions():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_versions)(request=request)
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
The request object. Request message for ModelService.ListModelVersions. |
`name` |
`str`
Required. The name of the model to list versions for. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelsPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_models():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_models)(request=request)
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
The request object. Request message for ModelService.ListModels. |
`parent` |
`str`
Required. The resource name of the Location to list the Models from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### merge_version_aliases

```
merge_version_aliases(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.MergeVersionAliasesRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
version_aliases: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model.Model
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
from google.cloud import aiplatform_v1beta1
def sample_merge_version_aliases():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[MergeVersionAliasesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MergeVersionAliasesRequest.html)(
name="name_value",
version_aliases=['version_aliases_value1', 'version_aliases_value2'],
)
# Make the request
response = client.[merge_version_aliases](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_merge_version_aliases)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.MergeVersionAliases. |
`name` |
`str`
Required. The name of the model version to merge aliases, with a version ID explicitly included. Example: |
`version_aliases` |
`MutableSequence[str]`
Required. The set of version aliases to merge. The alias should be at most 128 characters, and match |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### recommend_spec

```
recommend_spec(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.RecommendSpecRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.model_service.RecommendSpecResponse
```


Gets a Model's spec recommendations.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_recommend_spec():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RecommendSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecRequest.html)(
parent="parent_value",
gcs_uri="gcs_uri_value",
)
# Make the request
response = client.[recommend_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_recommend_spec)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.RecommendSpec. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ModelService.RecommendSpec. |

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

### update_explanation_dataset

```
update_explanation_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.UpdateExplanationDatasetRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
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


Incrementally update the dataset used for an examples model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_explanation_dataset():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateExplanationDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest.html)(
model="model_value",
)
# Make the request
operation = client.[update_explanation_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_update_explanation_dataset)(request=request)
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
The request object. Request message for ModelService.UpdateExplanationDataset. |
`model` |
`str`
Required. The resource name of the Model to update. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### update_model

```
update_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.UpdateModelRequest, dict
]
] = None,
*,
model: typing.Optional[google.cloud.aiplatform_v1beta1.types.model.Model] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model.Model
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
from google.cloud import aiplatform_v1beta1
def sample_update_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
model = aiplatform_v1beta1.[Model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.html)()
model.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelRequest.html)(
model=model,
)
# Make the request
response = client.[update_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_update_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.UpdateModel. |
`model` |
Required. The Model which replaces the resource on the server. When Model Versioning is enabled, the model.name will be used to determine whether to update the model or model version. 1. model.name with the @ value, e.g. models/123@1, refers to a version specific update. 2. model.name without the @ value, e.g. models/123, refers to a model update. 3. model.name with @-, e.g. models/123@-, refers to a model update. 4. Supported model fields: display_name, description; supported version-specific fields: version_description. Labels are supported in both scenarios. Both the model labels and the version labels are merged when a model is returned. When updating labels, if the request is for model-specific update, model label gets updated. Otherwise, version labels get updated. 5. A model name or model version name fields update mismatch will cause a precondition error. 6. One request cannot update both the model and the version fields. You must update them separately. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.cloud.aiplatform_v1beta1.types.model_service.UploadModelRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[google.cloud.aiplatform_v1beta1.types.model.Model] = None,
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


Uploads a Model artifact into Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_upload_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
model = aiplatform_v1beta1.[Model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.html)()
model.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelRequest.html)(
parent="parent_value",
model=model,
)
# Make the request
operation = client.[upload_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_upload_model)(request=request)
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
The request object. Request message for ModelService.UploadModel. |
`parent` |
`str`
Required. The resource name of the Location into which to upload the Model. Format: |
`model` |
Required. The Model to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicefeatureregistryserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient -->

# Class FeatureRegistryServiceClient (1.134.0)

```
FeatureRegistryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that handles CRUD and List for resources for FeatureRegistry.

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
`FeatureRegistryServiceTransport` |
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

### FeatureRegistryServiceClient

```
FeatureRegistryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature registry service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeatureRegistryServiceTransport,Callable[..., FeatureRegistryServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureRegistryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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


Creates a batch of Features in a given FeatureGroup.

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1beta1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_batch_create_features)(request=request)
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


Creates a new Feature in a given FeatureGroup.

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature)(request=request)
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

### create_feature_group

```
create_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.CreateFeatureGroupRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_group: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_group.FeatureGroup
] = None,
feature_group_id: typing.Optional[str] = None,
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


Creates a new FeatureGroup in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1beta1.[FeatureGroup](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.html)()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1beta1.[CreateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureGroupRequest.html)(
parent="parent_value",
feature_group=feature_group,
feature_group_id="feature_group_id_value",
)
# Make the request
operation = client.[create_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.CreateFeatureGroup. |
`parent` |
`str`
Required. The resource name of the Location to create FeatureGroups. Format: |
`feature_group` |
Required. The FeatureGroup to create. This corresponds to the |
`feature_group_id` |
`str`
Required. The ID to use for this FeatureGroup, which will become the final component of the FeatureGroup's resource name. This value may be up to 128 characters, and valid characters are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### create_feature_monitor

```
create_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.CreateFeatureMonitorRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_monitor: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_monitor.FeatureMonitor
] = None,
feature_monitor_id: typing.Optional[str] = None,
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


Creates a new FeatureMonitor in a given project, location and FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest.html)(
parent="parent_value",
feature_monitor_id="feature_monitor_id_value",
)
# Make the request
operation = client.[create_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_monitor)(request=request)
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
The request object. Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][]. |
`parent` |
`str`
Required. The resource name of FeatureGroup to create FeatureMonitor. Format: |
`feature_monitor` |
Required. The Monitor to create. This corresponds to the |
`feature_monitor_id` |
`str`
Required. The ID to use for this FeatureMonitor, which will become the final component of the FeatureGroup's resource name. This value may be up to 60 characters, and valid characters are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### create_feature_monitor_job

```
create_feature_monitor_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.CreateFeatureMonitorJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_monitor_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_monitor_job.FeatureMonitorJob
] = None,
feature_monitor_job_id: typing.Optional[int] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.feature_monitor_job.FeatureMonitorJob
```


Creates a new feature monitor job.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_feature_monitor_job():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureMonitorJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_feature_monitor_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_monitor_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [FeatureRegistryService.CreateFeatureMonitorJobRequest][]. |
`parent` |
`str`
Required. The resource name of FeatureMonitor to create FeatureMonitorJob. Format: |
`feature_monitor_job` |
Required. The Monitor to create. This corresponds to the |
`feature_monitor_job_id` |
`int`
Optional. Output only. System-generated ID for feature monitor job. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Vertex AI Feature Monitor Job. |

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature)(request=request)
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

### delete_feature_group

```
delete_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.DeleteFeatureGroupRequest,
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


Deletes a single FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.DeleteFeatureGroup. |
`name` |
`str`
Required. The name of the FeatureGroup to be deleted. Format: |
`force` |
`bool`
If set to true, any Features under this FeatureGroup will also be deleted. (Otherwise, the request will only work if the FeatureGroup has no Features.) This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_feature_monitor

```
delete_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.DeleteFeatureMonitorRequest,
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


Deletes a single FeatureMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureMonitorRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature_monitor)(request=request)
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
The request object. Request message for FeatureRegistryService.DeleteFeatureMonitor. |
`name` |
`str`
Required. The name of the FeatureMonitor to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### feature_group_path

`feature_group_path(project: str, location: str, feature_group: str) -> str`


Returns a fully-qualified feature_group string.

### feature_monitor_job_path

```
feature_monitor_job_path(
project: str,
location: str,
feature_group: str,
feature_monitor: str,
feature_monitor_job: str,
) -> str
```


Returns a fully-qualified feature_monitor_job string.

### feature_monitor_path

```
feature_monitor_path(
project: str, location: str, feature_group: str, feature_monitor: str
) -> str
```


Returns a fully-qualified feature_monitor string.

### feature_path

```
feature_path(
project: str, location: str, featurestore: str, entity_type: str, feature: str
) -> str
```


Returns a fully-qualified feature string.

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
`FeatureRegistryServiceClient` |
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
`FeatureRegistryServiceClient` |
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
`FeatureRegistryServiceClient` |
The constructed client. |

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature)(request=request)
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

### get_feature_group

```
get_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.GetFeatureGroupRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_group.FeatureGroup
```


Gets details of a single FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_group)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureRegistryService.GetFeatureGroup. |
`name` |
`str`
Required. The name of the FeatureGroup resource. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Vertex AI Feature Group. |

### get_feature_monitor

```
get_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.GetFeatureMonitorRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_monitor.FeatureMonitor
```


Gets details of a single FeatureMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_monitor)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureRegistryService.GetFeatureMonitor. |
`name` |
`str`
Required. The name of the FeatureMonitor resource. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Vertex AI Feature Monitor. |

### get_feature_monitor_job

```
get_feature_monitor_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.GetFeatureMonitorJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_monitor_job.FeatureMonitorJob
```


Get a feature monitor job.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_feature_monitor_job():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureMonitorJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_monitor_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_monitor_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureRegistryService.GetFeatureMonitorJob. |
`name` |
`str`
Required. The name of the FeatureMonitorJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Vertex AI Feature Monitor Job. |

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

### list_feature_groups

```
list_feature_groups(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsPager
)
```


Lists FeatureGroups in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_feature_groups():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureGroupsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_groups](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_groups)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureGroups. |
`parent` |
`str`
Required. The resource name of the Location to list FeatureGroups. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureRegistryService.ListFeatureGroups. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_monitor_jobs

```
list_feature_monitor_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsPager
)
```


List feature monitor jobs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_feature_monitor_jobs():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureMonitorJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_monitor_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_monitor_jobs)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureMonitorJobs. |
`parent` |
`str`
Required. The resource name of the FeatureMonitor to list FeatureMonitorJobs. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureRegistryService.ListFeatureMonitorJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_monitors

```
list_feature_monitors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsPager
)
```


Lists FeatureGroups in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_feature_monitors():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureMonitorsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_monitors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_monitors)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureMonitors. |
`parent` |
`str`
Required. The resource name of the FeatureGroup to list FeatureMonitors. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureRegistryService.ListFeatureMonitors. Iterating over this object will yield results and resolve additional pages automatically. |

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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesPager
)
```


Lists Features in a given FeatureGroup.

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_features)(request=request)
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

### parse_feature_group_path

`parse_feature_group_path(path: str) -> typing.Dict[str, str]`


Parses a feature_group path into its component segments.

### parse_feature_monitor_job_path

`parse_feature_monitor_job_path(path: str) -> typing.Dict[str, str]`


Parses a feature_monitor_job path into its component segments.

### parse_feature_monitor_path

`parse_feature_monitor_path(path: str) -> typing.Dict[str, str]`


Parses a feature_monitor path into its component segments.

### parse_feature_path

`parse_feature_path(path: str) -> typing.Dict[str, str]`


Parses a feature path into its component segments.

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
) -> google.api_core.operation.Operation
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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest.html)(
)
# Make the request
operation = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature)(request=request)
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### update_feature_group

```
update_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.UpdateFeatureGroupRequest,
dict,
]
] = None,
*,
feature_group: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_group.FeatureGroup
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


Updates the parameters of a single FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1beta1.[FeatureGroup](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.html)()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1beta1.[UpdateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupRequest.html)(
feature_group=feature_group,
)
# Make the request
operation = client.[update_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.UpdateFeatureGroup. |
`feature_group` |
Required. The FeatureGroup's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### update_feature_monitor

```
update_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.UpdateFeatureMonitorRequest,
dict,
]
] = None,
*,
feature_monitor: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_monitor.FeatureMonitor
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


Updates the parameters of a single FeatureMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorRequest.html)(
)
# Make the request
operation = client.[update_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature_monitor)(request=request)
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
The request object. Request message for FeatureRegistryService.UpdateFeatureMonitor. |
`feature_monitor` |
Required. The FeatureMonitor's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to specify the fields to be overwritten in the FeatureMonitor resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform______googlecloudaiplatform_v1typeslistmodelevaluationsli_0da402.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform______googlecloudaiplatform_v1typeslistmodelevaluationslic_146d5a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform -->

# Package aiplatform (1.134.0)

API documentation for `aiplatform`

package.

## Classes

[Artifact](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact)

Metadata Artifact resource for Vertex AI

[AutoMLForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLForecastingTrainingJob)

Class to train AutoML forecasting models.

The `AutoMLForecastingTrainingJob`

class uses the AutoML training method
to train and run a forecasting model. The `AutoML`

training method is a good
choice for most forecasting use cases. If your use case doesn't benefit from
the `Seq2seq`

or the `Temporal fusion transformer`

training method offered
by the
[ SequenceToSequencePlusForecastingTrainingJob](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob)
and
[

`TemporalFusionTransformerForecastingTrainingJob`

][https://cloud.google.com/python/docs/reference/aiplatform/latest/](https://cloud.google.com/python/docs/reference/aiplatform/latest/)

[google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob)) classes respectively, then

`AutoML`

is likely the best training method for
your forecasting predictions.For sample code that shows you how to use `AutoMLForecastingTrainingJob`

see
the [Create a training pipeline forecasting sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_sample.py)
on GitHub.

[AutoMLImageTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLImageTrainingJob)

Creates an AutoML image training job.

Use the `AutoMLImageTrainingJob`

class to create, train, and return an
image model. For more information about working with image data models
in Vertex AI, see [Image data](https://cloud.google.com/vertex-ai/docs/training-overview#image_data).

For an example of how to use the `AutoMLImageTrainingJob`

class, see the
tutorial in the [AutoML image
classification](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-text-classification-batch-prediction.ipynb)
notebook on GitHub.

[AutoMLTabularTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTabularTrainingJob)

Constructs a AutoML Tabular Training Job.

Example usage:

job = training_jobs.AutoMLTabularTrainingJob( display_name="my_display_name", optimization_prediction_type="classification", optimization_objective="minimize-log-loss", column_specs={"column_1": "auto", "column_2": "numeric"}, labels={'key': 'value'}, )

[AutoMLTextTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTextTrainingJob)

Constructs a AutoML Text Training Job.

[AutoMLVideoTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLVideoTrainingJob)

Constructs a AutoML Video Training Job.

[BatchPredictionJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob)

Retrieves a BatchPredictionJob resource and instantiates its representation.

[CustomContainerTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob)

Class to launch a Custom Training Job in Vertex AI using a Container.

[CustomJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob)

Vertex AI Custom Job.

[CustomPythonPackageTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob)

Class to launch a Custom Training Job in Vertex AI using a Python Package.

Use the `CustomPythonPackageTrainingJob`

class to use a Python package to
launch a custom training pipeline in Vertex AI. For an example of how to use
the `CustomPythonPackageTrainingJob`

class, see the tutorial in the [Custom
training using Python package, managed text dataset, and TensorFlow serving
container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb)
notebook.

[CustomTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob)

Class to launch a Custom Training Job in Vertex AI using a script.

Takes a training implementation as a python script and executes that script in Cloud Vertex AI Training.

[DeploymentResourcePool](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.DeploymentResourcePool)

Retrieves a DeploymentResourcePool.

[Endpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint)

Retrieves an endpoint resource.

[EntityType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType)

Public managed EntityType resource for Vertex AI.

[Execution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution)

Metadata Execution resource for Vertex AI

[Experiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment)

Represents a Vertex AI Experiment resource.

[ExperimentRun](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun)

A Vertex AI Experiment run.

[Feature](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature)

Managed feature resource for Vertex AI.

[Featurestore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore)

Managed featurestore resource for Vertex AI.

[HyperparameterTuningJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob)

Vertex AI Hyperparameter Tuning Job.

[ImageDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ImageDataset)

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


[MatchingEngineIndex](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndex)

Matching Engine index resource for Vertex AI.

[MatchingEngineIndexEndpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndexEndpoint)

Matching Engine index endpoint resource for Vertex AI.

[Model](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model)

Retrieves the model resource and instantiates its representation.

[ModelDeploymentMonitoringJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelDeploymentMonitoringJob)

Vertex AI Model Deployment Monitoring Job.

This class should be used in conjunction with the Endpoint class in order to configure model monitoring for deployed models.

[ModelEvaluation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelEvaluation)

Retrieves the ModelEvaluation resource and instantiates its representation.

[PipelineJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob)

Retrieves a PipelineJob resource and instantiates its representation.

[PipelineJobSchedule](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJobSchedule)

Retrieves a PipelineJobSchedule resource and instantiates its representation.

[PrivateEndpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint)

Represents a Vertex AI PrivateEndpoint resource.

[SequenceToSequencePlusForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob)

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

[TabularDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset)

A managed tabular dataset resource for Vertex AI.

Use this class to work with tabular datasets. You can use a CSV file, BigQuery, or a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html)
to create a tabular dataset. For more information about paging through
BigQuery data, see

[Read data with BigQuery API using pagination](https://cloud.google.com/bigquery/docs/paging-results). For more information about tabular data, see

[Tabular data](https://cloud.google.com/vertex-ai/docs/training-overview#tabular_data).

The following code shows you how to create and import a tabular dataset with a CSV file.

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


Contrary to unstructured datasets, creating and importing a tabular dataset can only be done in a single step.

If you create a tabular dataset with a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html),
you need to use a BigQuery table to stage the data for Vertex AI:

```
my_dataset = aiplatform.TabularDataset.create_from_dataframe(
df_source=my_pandas_dataframe,
staging_path=f"bq://{bq_dataset_id}.table-unique"
)
```


[TemporalFusionTransformerForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob)

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

[Tensorboard](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard)

Managed tensorboard resource for Vertex AI.

[TensorboardExperiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardExperiment)

Managed tensorboard resource for Vertex AI.

[TensorboardRun](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun)

Managed tensorboard resource for Vertex AI.

[TensorboardTimeSeries](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardTimeSeries)

Managed tensorboard resource for Vertex AI.

[TextDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TextDataset)

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


[TimeSeriesDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDataset)

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


[TimeSeriesDenseEncoderForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob)

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

[VideoDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.VideoDataset)

A managed video dataset resource for Vertex AI.

Use this class to work with a managed video dataset. To create a video dataset, you need a datasource in CSV format and a schema in YAML format. The CSV file and the schema are accessed in Cloud Storage buckets.

Use video data for the following objectives:

Classification. For more information, see Classification schema files. Action recognition. For more information, see Action recognition schema files. Object tracking. For more information, see Object tracking schema files. The following code shows you how to create and import a dataset to train a video classification model. The schema file you use depends on whether you use your video dataset for action classification, recognition, or object tracking.

```
my_dataset = aiplatform.VideoDataset.create(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=['gs://aip.schema.dataset.ioformat.video.classification.yaml']
)
```


## Packages Functions

### autolog

`autolog(disable=False)`


Enables autologging of parameters and metrics to Vertex Experiments.

After calling `aiplatform.autolog()`

, any metrics and parameters from
model training calls with supported ML frameworks will be automatically
logged to Vertex Experiments.

Using autologging requires setting an experiment and experiment_tensorboard.

Parameter |
|
|---|---|
Name |
Description |
`disable` |
`bool` Optional. Whether to disable autologging. Defaults to False. If set to True, this resets the MLFlow tracking URI to its previous state before autologging was called and remove logging filters. |

### end_run

```
end_run(
state: google.cloud.aiplatform_v1.types.execution.Execution.State = State.COMPLETE,
)
```


Ends the the current experiment run.

```
aiplatform.start_run('my-run')
...
aiplatform.end_run()
```


### end_upload_tb_log

`end_upload_tb_log()`


Ends the current TensorBoard uploader

```
aiplatform.start_upload_tb_log(...)
...
aiplatform.end_upload_tb_log()
```


### get_experiment_df

```
get_experiment_df(
experiment: typing.Optional[str] = None, *, include_time_series: bool = True
) -> pd.DataFrame
```


Returns a Pandas DataFrame of the parameters and metrics associated with one experiment.

Example:

```
aiplatform.init(experiment='exp-1')
aiplatform.start_run(run='run-1')
aiplatform.log_params({'learning_rate': 0.1})
aiplatform.log_metrics({'accuracy': 0.9})
aiplatform.start_run(run='run-2')
aiplatform.log_params({'learning_rate': 0.2})
aiplatform.log_metrics({'accuracy': 0.95})
aiplatform.get_experiment_df()
```


Will result in the following DataFrame:

```
experiment_name | run_name | param.learning_rate | metric.accuracy
exp-1 | run-1 | 0.1 | 0.9
exp-1 | run-2 | 0.2 | 0.95
```


Parameters |
|
|---|---|
Name |
Description |
`experiment` |
`str` Name of the Experiment to filter results. If not set, return results of current active experiment. |
`include_time_series` |
`bool` Optional. Whether or not to include time series metrics in df. Default is True. Setting to False will largely improve execution time and reduce quota contributing calls. Recommended when time series metrics are not needed or number of runs in Experiment is large. For time series metrics consider querying a specific run using get_time_series_data_frame. |

### get_experiment_model

```
get_experiment_model(
artifact_id: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel
```


Retrieves an existing ExperimentModel artifact given an artifact id.

Parameters |
|
|---|---|
Name |
Description |
`artifact_id` |
`str` Required. An artifact id of the ExperimentModel artifact. |
`metadata_store_id` |
`str` Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_id is a fully-qualified resource name, its metadata_store_id overrides this one. |
`project` |
`str` Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str` Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

### get_pipeline_df

`get_pipeline_df(pipeline: str) -> pd.DataFrame`


Returns a Pandas DataFrame of the parameters and metrics associated with one pipeline.

### init

```
init(
*,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
experiment: typing.Optional[str] = None,
experiment_description: typing.Optional[str] = None,
experiment_tensorboard: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform.tensorboard.tensorboard_resource.Tensorboard,
bool,
]
] = None,
staging_bucket: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
network: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
api_endpoint: typing.Optional[str] = None,
api_key: typing.Optional[str] = None,
api_transport: typing.Optional[str] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = None
)
```


Updates common initialization parameters with provided options.

Parameters |
|
|---|---|
Name |
Description |
`project` |
`str` The default project to use when making API calls. |
`location` |
`str` The default location to use when making API calls. If not set defaults to us-central-1. |
`experiment` |
`str` Optional. The experiment name. |
`experiment_description` |
`str` Optional. The description of the experiment. |
`experiment_tensorboard` |
`Union[str, tensorboard_resource.Tensorboard, bool]` Optional. The Vertex AI TensorBoard instance, Tensorboard resource name, or Tensorboard resource ID to use as a backing Tensorboard for the provided experiment. Example tensorboard resource name format: "projects/123/locations/us-central1/tensorboards/456" If |
`staging_bucket` |
`str` The default staging bucket to use to stage artifacts when making API calls. In the form gs://... |
`credentials` |
`google.auth.credentials.Credentials` The default custom credentials to use when making API calls. If not provided credentials will be ascertained from the environment. |
`encryption_spec_key_name` |
`Optional[str]` Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect a resource. Has the form: |
`network` |
`str` Optional. The full name of the Compute Engine network to which jobs and resources should be peered. E.g. "projects/12345/global/networks/myVPC". Private services access must already be configured for the network. If specified, all eligible jobs and resources created will be peered with this VPC. |
`service_account` |
`str` Optional. The service account used to launch jobs and deploy models. Jobs that use service_account: BatchPredictionJob, CustomJob, PipelineJob, HyperparameterTuningJob, CustomTrainingJob, CustomPythonPackageTrainingJob, CustomContainerTrainingJob, ModelEvaluationJob. |
`api_endpoint` |
`str` Optional. The desired API endpoint, e.g., us-central1-aiplatform.googleapis.com |
`api_key` |
`str` Optional. The API key to use for service calls. NOTE: Not all services support API keys. |
`api_transport` |
`str` Optional. The transport method which is either 'grpc' or 'rest'. NOTE: "rest" transport functionality is currently in a beta state (preview). |

### log

```
log(
*,
pipeline_job: typing.Optional[
google.cloud.aiplatform.pipeline_jobs.PipelineJob
] = None
)
```


Log Vertex AI Resources to the current experiment run.

```
aiplatform.start_run('my-run')
my_job = aiplatform.PipelineJob(...)
my_job.submit()
aiplatform.log(my_job)
```


Parameter |
|
|---|---|
Name |
Description |
`pipeline_job` |
`pipeline_jobs.PipelineJob` Optional. Vertex PipelineJob to associate to this Experiment Run. |

### log_classification_metrics

```
log_classification_metrics(
*,
labels: typing.Optional[typing.List[str]] = None,
matrix: typing.Optional[typing.List[typing.List[int]]] = None,
fpr: typing.Optional[typing.List[float]] = None,
tpr: typing.Optional[typing.List[float]] = None,
threshold: typing.Optional[typing.List[float]] = None,
display_name: typing.Optional[str] = None
) -> (
google.cloud.aiplatform.metadata.schema.google.artifact_schema.ClassificationMetrics
)
```


Create an artifact for classification metrics and log to ExperimentRun. Currently support confusion matrix and ROC curve.

```
my_run = aiplatform.ExperimentRun('my-run', experiment='my-experiment')
classification_metrics = my_run.log_classification_metrics(
display_name='my-classification-metrics',
labels=['cat', 'dog'],
matrix=[[9, 1], [1, 9]],
fpr=[0.1, 0.5, 0.9],
tpr=[0.1, 0.7, 0.9],
threshold=[0.9, 0.5, 0.1],
)
```


Parameters |
|
|---|---|
Name |
Description |
`labels` |
`List[str]` Optional. List of label names for the confusion matrix. Must be set if 'matrix' is set. |
`matrix` |
`List[List[int]` Optional. Values for the confusion matrix. Must be set if 'labels' is set. |
`fpr` |
`List[float]` Optional. List of false positive rates for the ROC curve. Must be set if 'tpr' or 'thresholds' is set. |
`tpr` |
`List[float]` Optional. List of true positive rates for the ROC curve. Must be set if 'fpr' or 'thresholds' is set. |
`threshold` |
`List[float]` Optional. List of thresholds for the ROC curve. Must be set if 'fpr' or 'tpr' is set. |
`display_name` |
`str` Optional. The user-defined name for the classification metric artifact. |

### log_metrics

`log_metrics(metrics: typing.Dict[str, typing.Union[float, int, str]])`


Log single or multiple Metrics with specified key and value pairs.

Metrics with the same key will be overwritten.

```
aiplatform.start_run('my-run', experiment='my-experiment')
aiplatform.log_metrics({'accuracy': 0.9, 'recall': 0.8})
```


Parameter |
|
|---|---|
Name |
Description |
`metrics` |
`Dict[str, Union[float, int, str]]` Required. Metrics key/value pairs. |

### log_model

```
log_model(
model: typing.Union[sklearn.base.BaseEstimator, xgb.Booster, tf.Module],
artifact_id: typing.Optional[str] = None,
*,
uri: typing.Optional[str] = None,
input_example: typing.Union[list, dict, pd.DataFrame, np.ndarray] = None,
display_name: typing.Optional[str] = None,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel
```


Saves a ML model into a MLMD artifact and log it to this ExperimentRun.

Supported model frameworks: sklearn, xgboost, tensorflow.

Example usage:

```
model = LinearRegression()
model.fit(X, y)
aiplatform.init(
project="my-project",
location="my-location",
staging_bucket="gs://my-bucket",
experiment="my-exp"
)
with aiplatform.start_run("my-run"):
aiplatform.log_model(model, "my-sklearn-model")
```


Parameters |
|
|---|---|
Name |
Description |
`model` |
`Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"]` Required. A machine learning model. |
`artifact_id` |
`str` Optional. The resource id of the artifact. This id must be globally unique in a metadataStore. It may be up to 63 characters, and valid characters are |
`uri` |
`str` Optional. A gcs directory to save the model file. If not provided, |
`input_example` |
`Union[list, dict, pd.DataFrame, np.ndarray]` Optional. An example of a valid model input. Will be stored as a yaml file in the gcs uri. Accepts list, dict, pd.DataFrame, and np.ndarray The value inside a list must be a scalar or list. The value inside a dict must be a scalar, list, or np.ndarray. |
`display_name` |
`str` Optional. The display name of the artifact. |
`metadata_store_id` |
`str` Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str` Optional. Project used to create this Artifact. Overrides project set in aiplatform.init. |
`location` |
`str` Optional. Location used to create this Artifact. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials used to create this Artifact. Overrides credentials set in aiplatform.init. |

### log_params

`log_params(params: typing.Dict[str, typing.Union[float, int, str]])`


Log single or multiple parameters with specified key and value pairs.

Parameters with the same key will be overwritten.

```
aiplatform.start_run('my-run')
aiplatform.log_params({'learning_rate': 0.1, 'dropout_rate': 0.2})
```


Parameter |
|
|---|---|
Name |
Description |
`params` |
`Dict[str, Union[float, int, str]]` Required. Parameter key/value pairs. |

### log_time_series_metrics

```
log_time_series_metrics(
metrics: typing.Dict[str, float],
step: typing.Optional[int] = None,
wall_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
)
```


Logs time series metrics to to this Experiment Run.

Requires the experiment or experiment run has a backing Vertex Tensorboard resource.

```
my_tensorboard = aiplatform.Tensorboard(...)
aiplatform.init(experiment='my-experiment', experiment_tensorboard=my_tensorboard)
aiplatform.start_run('my-run')
# increments steps as logged
for i in range(10):
aiplatform.log_time_series_metrics({'loss': loss})
# explicitly log steps
for i in range(10):
aiplatform.log_time_series_metrics({'loss': loss}, step=i)
```


Parameters |
|
|---|---|
Name |
Description |
`metrics` |
`Dict[str, Union[str, float]]` Required. Dictionary of where keys are metric names and values are metric values. |
`step` |
`int` Optional. Step index of this data point within the run. If not provided, the latest step amongst all time series metrics already logged will be used. |
`wall_time` |
`timestamp_pb2.Timestamp` Optional. Wall clock timestamp when this data point is generated by the end user. If not provided, this will be generated based on the value from time.time() |

### save_model

```
save_model(
model: typing.Union[sklearn.base.BaseEstimator, xgb.Booster, tf.Module],
artifact_id: typing.Optional[str] = None,
*,
uri: typing.Optional[str] = None,
input_example: typing.Union[list, dict, pd.DataFrame, np.ndarray] = None,
tf_save_model_kwargs: typing.Optional[typing.Dict[str, typing.Any]] = None,
display_name: typing.Optional[str] = None,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
staging_bucket: typing.Optional[str] = None
) -> google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel
```


Saves a ML model into a MLMD artifact.

Supported model frameworks: sklearn, xgboost, tensorflow.

Example usage: aiplatform.init(project="my-project", location="my-location", staging_bucket="gs://my-bucket") model = LinearRegression() model.fit(X, y) aiplatform.save_model(model, "my-sklearn-model")

Parameters |
|
|---|---|
Name |
Description |
`model` |
`Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"]` Required. A machine learning model. |
`artifact_id` |
`str` Optional. The resource id of the artifact. This id must be globally unique in a metadataStore. It may be up to 63 characters, and valid characters are |
`uri` |
`str` Optional. A gcs directory to save the model file. If not provided, |
`input_example` |
`Union[list, dict, pd.DataFrame, np.ndarray]` Optional. An example of a valid model input. Will be stored as a yaml file in the gcs uri. Accepts list, dict, pd.DataFrame, and np.ndarray The value inside a list must be a scalar or list. The value inside a dict must be a scalar, list, or np.ndarray. |
`tf_save_model_kwargs` |
`Dict[str, Any]` Optional. A dict of kwargs to pass to the model's save method. If saving a tf module, this will pass to "tf.saved_model.save" method. If saving a keras model, this will pass to "tf.keras.Model.save" method. |
`display_name` |
`str` Optional. The display name of the artifact. |
`metadata_store_id` |
`str` Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str` Optional. Project used to create this Artifact. Overrides project set in aiplatform.init. |
`location` |
`str` Optional. Location used to create this Artifact. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials used to create this Artifact. Overrides credentials set in aiplatform.init. |
`staging_bucket` |
`str` Optional. The staging bucket used to save the model. If not provided, the staging bucket set in aiplatform.init will be used. A staging bucket or uri is required for saving a model. |

### start_execution

```
start_execution(
*,
schema_title: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
resource_id: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict[str, typing.Any]] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
resume: bool = False,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.execution.Execution
```


Create and starts a new Metadata Execution or resumes a previously created Execution.

To start a new execution:

```
with aiplatform.start_execution(schema_title='system.ContainerExecution', display_name='trainer) as exc:
exc.assign_input_artifacts([my_artifact])
model = aiplatform.Artifact.create(uri='gs://my-uri', schema_title='system.Model')
exc.assign_output_artifacts([model])
```


To continue a previously created execution:

```
with aiplatform.start_execution(resource_id='my-exc', resume=True) as exc:
...
```


Parameters |
|
|---|---|
Name |
Description |
`schema_title` |
`str` Optional. schema_title identifies the schema title used by the Execution. Required if starting a new Execution. |
`resource_id` |
`str` Optional. The <resource_id> portion of the Execution name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/executions/<resource_id>. |
`display_name` |
`str` Optional. The user-defined name of the Execution. |
`schema_version` |
`str` Optional. schema_version specifies the version used by the Execution. If not set, defaults to use the latest version. |
`metadata` |
`Dict` Optional. Contains the metadata information that will be stored in the Execution. |
`description` |
`str` Optional. Describes the purpose of the Execution to be created. |
`metadata_store_id` |
`str` Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str` Optional. Project used to create this Execution. Overrides project set in aiplatform.init. |
`location` |
`str` Optional. Location used to create this Execution. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials used to create this Execution. Overrides credentials set in aiplatform.init. |

### start_run

```
start_run(
run: str,
*,
tensorboard: typing.Optional[
typing.Union[
google.cloud.aiplatform.tensorboard.tensorboard_resource.Tensorboard, str
]
] = None,
resume=False
) -> google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun
```


Start a run to current session.

```
aiplatform.init(experiment='my-experiment')
aiplatform.start_run('my-run')
aiplatform.log_params({'learning_rate':0.1})
```


Use as context manager. Run will be ended on context exit:

```
aiplatform.init(experiment='my-experiment')
with aiplatform.start_run('my-run') as my_run:
my_run.log_params({'learning_rate':0.1})
```


Resume a previously started run:

```
aiplatform.init(experiment='my-experiment')
with aiplatform.start_run('my-run', resume=True) as my_run:
my_run.log_params({'learning_rate':0.1})
```


Parameters |
|
|---|---|
Name |
Description |
`run` |
`str` Required. Name of the run to assign current session with. |
`resume` |
`bool` Whether to resume this run. If False a new run will be created. |

### start_upload_tb_log

```
start_upload_tb_log(
tensorboard_experiment_name: str,
logdir: str,
tensorboard_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
experiment_display_name: typing.Optional[str] = None,
run_name_prefix: typing.Optional[str] = None,
description: typing.Optional[str] = None,
allowed_plugins: typing.Optional[typing.FrozenSet[str]] = None,
)
```


Continues to listen for new data in the logdir and uploads when it appears.

Note that after calling `start_upload_tb_log()`

your thread will kept alive even if
an exception is thrown. To ensure the thread gets shut down, put any code after
`start_upload_tb_log()`

and before `end_upload_tb_log()`

in a `try`

statement, and call
`end_upload_tb_log()`

in `finally`

.

```
Sample usage:
aiplatform.init(location='us-central1', project='my-project')
aiplatform.start_upload_tb_log(tensorboard_id='123',tensorboard_experiment_name='my-experiment',logdir='my-logdir')
try:
# your code here
finally:
aiplatform.end_upload_tb_log()
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_name` |
`str` Required. Name of this tensorboard experiment. Unique to the given projects/{project}/locations/{location}/tensorboards/{tensorboard_id}. |
`logdir` |
`str` Required. path of the log directory to upload |
`tensorboard_id` |
`str` Optional. TensorBoard ID. If not set, tensorboard_id in aiplatform.init will be used. |
`project` |
`str` Optional. Project the TensorBoard is in. If not set, project set in aiplatform.init will be used. |
`location` |
`str` Optional. Location the TensorBoard is in. If not set, location set in aiplatform.init will be used. |
`experiment_display_name` |
`str` Optional. The display name of the experiment. |
`run_name_prefix` |
`str` Optional. If present, all runs created by this invocation will have their name prefixed by this value. |
`description` |
`str` Optional. String description to assign to the experiment. |
`allowed_plugins` |
`FrozenSet[str]` Optional. List of additional allowed plugin names. |

### upload_tb_log

```
upload_tb_log(
tensorboard_experiment_name: str,
logdir: str,
tensorboard_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
experiment_display_name: typing.Optional[str] = None,
run_name_prefix: typing.Optional[str] = None,
description: typing.Optional[str] = None,
verbosity: typing.Optional[int] = 1,
allowed_plugins: typing.Optional[typing.FrozenSet[str]] = None,
)
```


upload only the existing data in the logdir and then return immediately

```
Sample usage:
aiplatform.init(location='us-central1', project='my-project')
aiplatform.upload_tb_log(tensorboard_id='123',tensorboard_experiment_name='my-experiment',logdir='my-logdir')
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_name` |
`str` Required. Name of this tensorboard experiment. Unique to the given projects/{project}/locations/{location}/tensorboards/{tensorboard_id} |
`logdir` |
`str` Required. The location of the TensorBoard logs that resides either in the local file system or Cloud Storage |
`tensorboard_id` |
`str` Optional. TensorBoard ID. If not set, tensorboard_id in aiplatform.init will be used. |
`project` |
`str` Optional. Project the TensorBoard is in. If not set, project set in aiplatform.init will be used. |
`location` |
`str` Optional. Location the TensorBoard is in. If not set, location set in aiplatform.init will be used. |
`experiment_display_name` |
`str` Optional. The display name of the experiment. |
`run_name_prefix` |
`str` Optional. If present, all runs created by this invocation will have their name prefixed by this value. |
`description` |
`str` Optional. String description to assign to the experiment. |
`verbosity` |
`str` Optional. Level of verbosity, an integer. Supported value: 0 - No upload statistics is printed. 1 - Print upload statistics while uploading data (default). |
`allowed_plugins` |
`FrozenSet[str]` Optional. List of additional allowed plugin names. |


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typeslistmodelevaluationslicesresponse_googleclouda_8fcec6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typeslistmodelevaluationslicesresponse_googlecloudai_486060.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistmodelevaluationslicesresponse_googlecloudaip_e9f591.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistmodelevaluationslicesresponse_googlecloudaipl_b12c81.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmodelevaluationslicesresponse_googlecloudaipla_d734fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelevaluationslicesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse -->

# Class ListModelEvaluationSlicesResponse (1.134.0)

```
ListModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluationSlices.

## Attributes |
|
|---|---|
Name |
Description |
`model_evaluation_slices` |
`MutableSequence[`
List of ModelEvaluations in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelEvaluationSlicesRequest.page_token to obtain that page. |

## Methods

### ListModelEvaluationSlicesResponse

```
ListModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluationSlices.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassessdataresponsebatchpredictionresourceusageassessmentresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataResponse.BatchPredictionResourceUsageAssessmentResult -->

# Class BatchPredictionResourceUsageAssessmentResult (1.134.0)

```
BatchPredictionResourceUsageAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the batch prediction resource usage assessment.

## Attributes |
|
|---|---|
Name |
Description |
`token_count` |
`int`
Number of tokens in the batch prediction dataset. |
`audio_token_count` |
`int`
Number of audio tokens in the batch prediction dataset. |

## Methods

### BatchPredictionResourceUsageAssessmentResult

```
BatchPredictionResourceUsageAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the batch prediction resource usage assessment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexamples.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Examples -->

# Class Examples (1.134.0)

`Examples(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Example-based explainability that returns the nearest neighbors from the provided dataset.

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
`example_gcs_source` |
The Cloud Storage input instances. This field is a member of `oneof` _ `source` .
|
`nearest_neighbor_search_config` |
`google.protobuf.struct_pb2.Value`
The full configuration for the generated index, the semantics are the same as metadata and should match `NearestNeighborSearchConfig ` __.
This field is a member of `oneof` _ `config` .
|
`presets` |
Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality. This field is a member of `oneof` _ `config` .
|
`neighbor_count` |
`int`
The number of neighbors to return when querying for examples. |

## Classes

### ExampleGcsSource

`ExampleGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage input instances.

## Methods

### Examples

`Examples(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Example-based explainability that returns the nearest neighbors from the provided dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeserroranalysisannotationattributeditem_google_e22270.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeserroranalysisannotationattributeditem_googlec_96ebcd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeserroranalysisannotationattributeditem.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ErrorAnalysisAnnotation.AttributedItem -->

# Class AttributedItem (1.134.0)

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

## Attributes |
|
|---|---|
Name |
Description |
`annotation_resource_name` |
`str`
The unique ID for each annotation. Used by FE to allocate the annotation in DB. |
`distance` |
`float`
The distance of this item to the annotation. |

## Methods

### AttributedItem

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelversioncheckpointsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse -->

# Class ListModelVersionCheckpointsResponse (1.134.0)

```
ListModelVersionCheckpointsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelVersionCheckpoints

## Attributes |
|
|---|---|
Name |
Description |
`checkpoints` |
`MutableSequence[`
List of Model Version checkpoints. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListModelVersionCheckpointsRequest.page_token to obtain that page. |

## Methods

### ListModelVersionCheckpointsResponse

```
ListModelVersionCheckpointsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelVersionCheckpoints


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreplicatedvoiceconfig_googlecloudaiplatform_v_809bd3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreplicatedvoiceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReplicatedVoiceConfig -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatavisualizationpolarity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization.Polarity -->

# Class Polarity (1.134.0)

`Polarity(value)`


Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

## Enums |
|
|---|---|
Name |
Description |
`POLARITY_UNSPECIFIED` |
Default value. This is the same as POSITIVE. |
`POSITIVE` |
Highlights the pixels/outlines that were most influential to the model's prediction. |
`NEGATIVE` |
Setting polarity to negative highlights areas that does not lead to the models's current prediction. |
`BOTH` |
Shows both positive and negative attributions. |

## Methods

### Polarity

`Polarity(value)`


Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesragmanageddbconfigbasic_googlecloudaiplatform_v1_34f755.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesragmanageddbconfigbasic_googlecloudaiplatform_v1b_848354.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragmanageddbconfigbasic_googlecloudaiplatform_v1be_1939ef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragmanageddbconfigbasic.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig.Basic -->

# Class Basic (1.134.0)

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.

## Methods

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigrateautomlmodelconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateAutomlModelConfig -->

# Class MigrateAutomlModelConfig (1.134.0)

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. Full resource name of automl Model. Format: `projects/{project}/locations/{location}/models/{model}` .
|
`model_display_name` |
`str`
Optional. Display name of the model in Vertex AI. System will pick a display name if unspecified. |

## Methods

### MigrateAutomlModelConfig

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesresourcepool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResourcePool -->

# Class ResourcePool (1.134.0)

`ResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a group of resources of the same type, for example machine type, disk, and accelerators, in a PersistentResource.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Immutable. The unique ID in a PersistentResource for referring to this resource pool. User can specify it if necessary. Otherwise, it's generated automatically. |
`machine_spec` |
Required. Immutable. The specification of a single machine. |
`replica_count` |
`int`
Optional. The total number of machines to use for this resource pool. This field is a member of `oneof` _ `_replica_count` .
|
`disk_spec` |
Optional. Disk spec for the machine in this node pool. |
`used_replica_count` |
`int`
Output only. The number of machines currently in use by training jobs for this resource pool. Will replace idle_replica_count. |
`autoscaling_spec` |
Optional. Optional spec to configure GKE or Ray-on-Vertex autoscaling |

## Classes

### AutoscalingSpec

`AutoscalingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The min/max number of replicas allowed if enabling autoscaling

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ResourcePool

`ResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a group of resources of the same type, for example machine type, disk, and accelerators, in a PersistentResource.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeleteartifactrequest_googlecloudaiplatform_v1bet_8d0a4f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeleteartifactrequest_googlecloudaiplatform_v1beta_e9ba45.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteArtifactRequest -->

# Class DeleteArtifactRequest (1.134.0)

`DeleteArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Artifact to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`etag` |
`str`
Optional. The etag of the Artifact to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED_PRECONDITION. |

## Methods

### DeleteArtifactRequest

`DeleteArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteArtifact.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatehyperparametertuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateHyperparameterTuningJobRequest -->

# Class CreateHyperparameterTuningJobRequest (1.134.0)

```
CreateHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateHyperparameterTuningJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the HyperparameterTuningJob in. Format: `projects/{project}/locations/{location}`
|
`hyperparameter_tuning_job` |
Required. The HyperparameterTuningJob to create. |

## Methods

### CreateHyperparameterTuningJobRequest

```
CreateHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateHyperparameterTuningJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Explanation -->

# Class Explanation (1.134.0)

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation of a prediction (provided in PredictResponse.predictions) produced by the Model on a given instance.

## Attributes |
|
|---|---|
Name |
Description |
`attributions` |
`MutableSequence[`
Output only. Feature attributions grouped by predicted outputs. For Models that predict only one output, such as regression Models that predict only one score, there is only one attibution that explains the predicted output. For Models that predict multiple outputs, such as multiclass Models that predict multiple classes, each element explains one specific item. Attribution.output_index can be used to identify which output this attribution is explaining. By default, we provide Shapley values for the predicted class. However, you can configure the explanation request to generate Shapley values for any other classes too. For example, if a model predicts a probability of `0.4` for
approving a loan application, the model's decision is to
reject the application since
`p(reject) = 0.6 > p(approve) = 0.4` , and the default
Shapley values would be computed for rejection decision and
not approval, even though the latter might be the positive
class.
If users set
ExplanationParameters.top_k,
the attributions are sorted by
`instance_output_value][Attributions.instance_output_value]`
in descending order. If
ExplanationParameters.output_indices
is specified, the attributions are stored by
Attribution.output_index
in the same order as they appear in the output_indices.
|
`neighbors` |
`MutableSequence[`
Output only. List of the nearest neighbors for example-based explanations. For models deployed with the examples explanations feature enabled, the attributions field is empty and instead the neighbors field is populated. |

## Methods

### Explanation

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation of a prediction (provided in PredictResponse.predictions) produced by the Model on a given instance.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesauthconfigoidcconfig__googlecloudaiplatform_d3f268.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesauthconfigoidcconfig__googlecloudaiplatform__e0ab5c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesauthconfigoidcconfig__googlecloudaiplatform_v_56fd52.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesauthconfigoidcconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig.OidcConfig -->

# Class OidcConfig (1.134.0)

`OidcConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user OIDC auth.

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
`id_token` |
`str`
OpenID Connect formatted ID token for extension endpoint. Only used to propagate token from [[ExecuteExtensionRequest.runtime_auth_config]] at request time. This field is a member of `oneof` _ `oidc_config` .
|
`service_account` |
`str`
The service account used to generate an OpenID Connect (OIDC)-compatible JWT token signed by the Google OIDC Provider (accounts.google.com) for extension endpoint (https://cloud.google.com/iam/docs/create-short-lived-credentials-direct#sa-credentials-oidc). - The audience for the token will be set to the URL in the server url defined in the OpenApi spec. - If the service account is provided, the service account should grant `iam.serviceAccounts.getOpenIdToken`
permission to Vertex AI Extension Service Agent
(https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents).
This field is a member of `oneof` _ `oidc_config` .
|

## Methods

### OidcConfig

`OidcConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user OIDC auth.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestensorboardtimeseriesvaluetype_googlecloudaip_000efe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardtimeseriesvaluetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries.ValueType -->

# Class ValueType (1.134.0)

`ValueType(value)`


An enum representing the value type of a TensorboardTimeSeries.

## Enums |
|
|---|---|
Name |
Description |
`VALUE_TYPE_UNSPECIFIED` |
The value type is unspecified. |
`SCALAR` |
Used for TensorboardTimeSeries that is a list of scalars. E.g. accuracy of a model over epochs/time. |
`TENSOR` |
Used for TensorboardTimeSeries that is a list of tensors. E.g. histograms of weights of layer in a model over epoch/time. |
`BLOB_SEQUENCE` |
Used for TensorboardTimeSeries that is a list of blob sequences. E.g. set of sample images with labels over epochs/time. |

## Methods

### ValueType

`ValueType(value)`


An enum representing the value type of a TensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationcolormap.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.ColorMap -->

# Class ColorMap (1.134.0)

`ColorMap(value)`


The color scheme used for highlighting areas.

## Enums |
|
|---|---|
Name |
Description |
`COLOR_MAP_UNSPECIFIED` |
Should not be used. |
`PINK_GREEN` |
Positive: green. Negative: pink. |
`VIRIDIS` |
Viridis color map: A perceptually uniform color mapping which is easier to see by those with colorblindness and progresses from yellow to green to blue. Positive: yellow. Negative: blue. |
`RED` |
Positive: red. Negative: red. |
`GREEN` |
Positive: green. Negative: green. |
`RED_GREEN` |
Positive: green. Negative: red. |
`PINK_WHITE_GREEN` |
PiYG palette. |

## Methods

### ColorMap

`ColorMap(value)`


The color scheme used for highlighting areas.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreadindexdatapointsrequest_googlecloudaiplatform__aae5f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadindexdatapointsrequest_googlecloudaiplatform_v_a38f02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadindexdatapointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadIndexDatapointsRequest -->

# Class ReadIndexDatapointsRequest (1.134.0)

`ReadIndexDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The request message for MatchService.ReadIndexDatapoints.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the index endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
The ID of the DeployedIndex that will serve the request. |
`ids` |
`MutableSequence[str]`
IDs of the datapoints to be searched for. |

## Methods

### ReadIndexDatapointsRequest

`ReadIndexDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The request message for MatchService.ReadIndexDatapoints.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service -->

# Package index_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.index_service`

package.

## Classes

[IndexServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceAsyncClient)

A service for creating and managing Vertex AI's Index resources.

[IndexServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient)

A service for creating and managing Vertex AI's Index resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers)

API documentation for `aiplatform_v1beta1.services.index_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestimeseriesdata_googlecloudaiplatform_v1typesc_45dd49.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestimeseriesdata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimeSeriesData -->

# Class TimeSeriesData (1.134.0)

`TimeSeriesData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


All the data stored in a TensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series_id` |
`str`
Required. The ID of the TensorboardTimeSeries, which will become the final component of the TensorboardTimeSeries' resource name |
`value_type` |
Required. Immutable. The value type of this time series. All the values in this time series data must match this value type. |
`values` |
`MutableSequence[`
Required. Data points in this time series. |

## Methods

### TimeSeriesData

`TimeSeriesData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


All the data stored in a TensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatehyperparametertuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateHyperparameterTuningJobRequest -->

# Class CreateHyperparameterTuningJobRequest (1.134.0)

```
CreateHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateHyperparameterTuningJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the HyperparameterTuningJob in. Format: `projects/{project}/locations/{location}`
|
`hyperparameter_tuning_job` |
Required. The HyperparameterTuningJob to create. |

## Methods

### CreateHyperparameterTuningJobRequest

```
CreateHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateHyperparameterTuningJob.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespausemodeldeploymentmonitoringjobrequest_go_39c3c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespausemodeldeploymentmonitoringjobrequest_goo_571f3a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespausemodeldeploymentmonitoringjobrequest_goog_2aacf2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespausemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseModelDeploymentMonitoringJobRequest -->

# Class PauseModelDeploymentMonitoringJobRequest (1.134.0)

```
PauseModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.PauseModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to pause. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### PauseModelDeploymentMonitoringJobRequest

```
PauseModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.PauseModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service -->

# Package dataset_service (1.134.0)

API documentation for `aiplatform_v1.services.dataset_service`

package.

## Classes

[DatasetServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceAsyncClient)

The service that manages Vertex AI Dataset and its child resources.

[DatasetServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.DatasetServiceClient)

The service that manages Vertex AI Dataset and its child resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers)

API documentation for `aiplatform_v1.services.dataset_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeatureonlinestoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresRequest -->

# Class ListFeatureOnlineStoresRequest (1.134.0)

```
ListFeatureOnlineStoresRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list FeatureOnlineStores. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the FeatureOnlineStores that match the filter expression. The following fields are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
Examples:
- `create_time > "2020-01-01" OR update_time > "2020-01-01"`
FeatureOnlineStores created or updated after 2020-01-01.
- `labels.env = "prod"` FeatureOnlineStores with label
"env" set to "prod".
|
`page_size` |
`int`
The maximum number of FeatureOnlineStores to return. The service may return fewer than this value. If unspecified, at most 100 FeatureOnlineStores will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureOnlineStores call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureOnlineStores must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields: - `create_time`
- `update_time`
|

## Methods

### ListFeatureOnlineStoresRequest

```
ListFeatureOnlineStoresRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesindexdatapointsparseembedding_googlecloudaip_c22f9a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesindexdatapointsparseembedding_googlecloudaipl_20070b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesindexdatapointsparseembedding.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint.SparseEmbedding -->

# Class SparseEmbedding (1.134.0)

`SparseEmbedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. The list of embedding values of the sparse vector. |
`dimensions` |
`MutableSequence[int]`
Required. The list of indexes for the embedding values of the sparse vector. |

## Methods

### SparseEmbedding

`SparseEmbedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatenotebookexecutionjoboperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookExecutionJobOperationMetadata -->

# Class CreateNotebookExecutionJobOperationMetadata (1.134.0)

```
CreateNotebookExecutionJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookExecutionJob.

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

### CreateNotebookExecutionJobOperationMetadata

```
CreateNotebookExecutionJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookExecutionJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesencryptionspec_googlecloudaiplatform_v1typesupload_8c01ca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesencryptionspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EncryptionSpec -->

# Class EncryptionSpec (1.134.0)

`EncryptionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a customer-managed encryption key spec that can be applied to a top-level resource.

## Attribute |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
Required. The Cloud KMS resource identifier of the customer managed encryption key used to protect a resource. Has the form: `projects/my-project/locations/my-region/keyRings/my-kr/cryptoKeys/my-key` .
The key needs to be in the same region as where the compute
resource is created.
|

## Methods

### EncryptionSpec

`EncryptionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a customer-managed encryption key spec that can be applied to a top-level resource.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesuploadragfilerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileRequest -->

# Class UploadRagFileRequest (1.134.0)

`UploadRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UploadRagFile.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the RagCorpus resource into which to upload the file. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`rag_file` |
Required. The RagFile to upload. |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. |

## Methods

### UploadRagFileRequest

`UploadRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UploadRagFile.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typescandidate__googlecloudaiplatform_v1beta1typesc_b23a64.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescandidate__googlecloudaiplatform_v1beta1typescr_74ab9b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescandidate__googlecloudaiplatform_v1beta1typescre_e59648.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescandidate__googlecloudaiplatform_v1beta1typescrea_b4e8e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescandidate__googlecloudaiplatform_v1beta1typescreat_bda863.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescandidate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Candidate -->

# Class Candidate (1.134.0)

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A response candidate generated from the model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`int`
Output only. Index of the candidate. |
`content` |
Output only. Content parts of the candidate. |
`score` |
`float`
Output only. Confidence score of the candidate. |
`avg_logprobs` |
`float`
Output only. Average log probability score of the candidate. |
`logprobs_result` |
Output only. Log-likelihood scores for the response tokens and top tokens |
`finish_reason` |
Output only. The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens. |
`safety_ratings` |
`MutableSequence[`
Output only. List of ratings for the safety of a response candidate. There is at most one rating per category. |
`finish_message` |
`str`
Output only. Describes the reason the mode stopped generating tokens in more detail. This is only filled when `finish_reason` is set.
This field is a member of `oneof` _ `_finish_message` .
|
`citation_metadata` |
Output only. Source attribution of the generated content. |
`grounding_metadata` |
Output only. Metadata specifies sources used to ground generated content. |
`url_context_metadata` |
Output only. Metadata related to url context retrieval tool. |

## Classes

### FinishReason

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

## Methods

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A response candidate generated from the model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatenotebookexecutionjoboperationmetadata_g_356c4d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatenotebookexecutionjoboperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookExecutionJobOperationMetadata -->

# Class CreateNotebookExecutionJobOperationMetadata (1.134.0)

```
CreateNotebookExecutionJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookExecutionJob.

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

### CreateNotebookExecutionJobOperationMetadata

```
CreateNotebookExecutionJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookExecutionJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigrateresourcerequestmigrateautomlmodelconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateAutomlModelConfig -->

# Class MigrateAutomlModelConfig (1.134.0)

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. Full resource name of automl Model. Format: `projects/{project}/locations/{location}/models/{model}` .
|
`model_display_name` |
`str`
Optional. Display name of the model in Vertex AI. System will pick a display name if unspecified. |

## Methods

### MigrateAutomlModelConfig

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesresourcepool__googlecloudaiplatform_v1typesli_b16e41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesresourcepool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourcePool -->

# Class ResourcePool (1.134.0)

`ResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a group of resources of the same type, for example machine type, disk, and accelerators, in a PersistentResource.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Immutable. The unique ID in a PersistentResource for referring to this resource pool. User can specify it if necessary. Otherwise, it's generated automatically. |
`machine_spec` |
Required. Immutable. The specification of a single machine. |
`replica_count` |
`int`
Optional. The total number of machines to use for this resource pool. This field is a member of `oneof` _ `_replica_count` .
|
`disk_spec` |
Optional. Disk spec for the machine in this node pool. |
`used_replica_count` |
`int`
Output only. The number of machines currently in use by training jobs for this resource pool. Will replace idle_replica_count. |
`autoscaling_spec` |
Optional. Optional spec to configure GKE or Ray-on-Vertex autoscaling |

## Classes

### AutoscalingSpec

`AutoscalingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The min/max number of replicas allowed if enabling autoscaling

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ResourcePool

`ResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a group of resources of the same type, for example machine type, disk, and accelerators, in a PersistentResource.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistfeatureviewsyncsresponse_googlecloudaiplatform_ded8ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeatureviewsyncsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse -->

# Class ListFeatureViewSyncsResponse (1.134.0)

```
ListFeatureViewSyncsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view_syncs` |
`MutableSequence[`
The FeatureViewSyncs matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureViewSyncsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureViewSyncsResponse

```
ListFeatureViewSyncsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteExecutionRequest -->

# Class DeleteExecutionRequest (1.134.0)

`DeleteExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteExecution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Execution to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`etag` |
`str`
Optional. The etag of the Execution to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED_PRECONDITION. |

## Methods

### DeleteExecutionRequest

`DeleteExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteExecution.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmodeldeploymentmonitoringjoblatestmonitoringpipe_d2fecf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodeldeploymentmonitoringjoblatestmonitoringpipel_7bfdd9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentmonitoringjoblatestmonitoringpipeli_123810.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringjoblatestmonitoringpipelinemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob.LatestMonitoringPipelineMetadata -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjobdataformrepositorysource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.DataformRepositorySource -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchfeaturesresponse_googlecloudaiplatform__e48801.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchfeaturesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse -->

# Class SearchFeaturesResponse (1.134.0)

`SearchFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.SearchFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
The Features matching the request. Fields returned: - `name`
- `description`
- `labels`
- `create_time`
- `update_time`
|
`next_page_token` |
`str`
A token, which can be sent as SearchFeaturesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### SearchFeaturesResponse

`SearchFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.SearchFeatures.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnotebookexecutionjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsResponse -->

# Class ListNotebookExecutionJobsResponse (1.134.0)

```
ListNotebookExecutionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [NotebookService.CreateNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`notebook_execution_jobs` |
`MutableSequence[`
List of NotebookExecutionJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookExecutionJobsRequest.page_token to obtain that page. |

## Methods

### ListNotebookExecutionJobsResponse

```
ListNotebookExecutionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [NotebookService.CreateNotebookExecutionJob]


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesassessdatarequesttuningvalidationassessmentc_a12e45.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesassessdatarequesttuningvalidationassessmentco_4e137a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassessdatarequesttuningvalidationassessmentconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.TuningValidationAssessmentConfig -->

# Class TuningValidationAssessmentConfig (1.134.0)

```
TuningValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning validation assessment.

## Attributes |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. The name of the model used for tuning. |
`dataset_usage` |
Required. The dataset usage (e.g. training/validation). |

## Classes

### DatasetUsage

`DatasetUsage(value)`


The dataset usage (e.g. training/validation).

## Methods

### TuningValidationAssessmentConfig

```
TuningValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning validation assessment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescounttokensresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CountTokensResponse -->

# Class CountTokensResponse (1.134.0)

`CountTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.CountTokens][].

## Attributes |
|
|---|---|
Name |
Description |
`total_tokens` |
`int`
The total number of tokens counted across all instances from the request. |
`total_billable_characters` |
`int`
The total number of billable characters counted across all instances from the request. |
`prompt_tokens_details` |
`MutableSequence[`
Output only. List of modalities that were processed in the request input. |

## Methods

### CountTokensResponse

`CountTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.CountTokens][].


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletemodeldeploymentmonitoringjobrequest_goo_b055d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelDeploymentMonitoringJobRequest -->

# Class DeleteModelDeploymentMonitoringJobRequest (1.134.0)

```
DeleteModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### DeleteModelDeploymentMonitoringJobRequest

```
DeleteModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnastrialstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasTrial.State -->

# Class State (1.134.0)

`State(value)`


Describes a NasTrial state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The NasTrial state is unspecified. |
`REQUESTED` |
Indicates that a specific NasTrial has been requested, but it has not yet been suggested by the service. |
`ACTIVE` |
Indicates that the NasTrial has been suggested. |
`STOPPING` |
Indicates that the NasTrial should stop according to the service. |
`SUCCEEDED` |
Indicates that the NasTrial is completed successfully. |
`INFEASIBLE` |
Indicates that the NasTrial should not be attempted again. The service will set a NasTrial to INFEASIBLE when it's done but missing the final_measurement. |

## Methods

### State

`State(value)`


Describes a NasTrial state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformbatchpredictionjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob -->

# Class BatchPredictionJob (1.134.0)

```
BatchPredictionJob(
batch_prediction_job_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves a BatchPredictionJob resource and instantiates its representation.

## Parameter |
|
|---|---|
Name |
Description |
`batch_prediction_job_name` |
`str`
Required. A fully-qualified BatchPredictionJob resource name or ID. Example: "projects/.../locations/.../batchPredictionJobs/456" or "456" when project and location are initialized or passed. |

## Properties

### completion_stats

Statistics on completed and failed prediction instances.

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

### output_info

Information describing the output of this job, including output location into which prediction output is written.

This is only available for batch prediction jobs that have run successfully.

### partial_failures

Partial failures encountered. For example, single files that can't be read. This field never exceeds 20 entries. Status details fields contain standard GCP error details.

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

## Methods

### cancel

`cancel() -> None`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

### create

```
create(
job_display_name: str,
model_name: typing.Union[str, google.cloud.aiplatform.models.Model],
instances_format: str = "jsonl",
predictions_format: str = "jsonl",
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bigquery_source: typing.Optional[str] = None,
gcs_destination_prefix: typing.Optional[str] = None,
bigquery_destination_prefix: typing.Optional[str] = None,
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
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
batch_size: typing.Optional[int] = None,
model_monitoring_objective_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
] = None,
model_monitoring_alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.AlertConfig
] = None,
analysis_instance_schema_uri: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.BatchPredictionJob
```


Create a batch prediction job.

Parameters |
|
|---|---|
Name |
Description |
`job_display_name` |
`str`
Required. The user-defined name of the BatchPredictionJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`model_name` |
`Union[str, aiplatform.Model]`
Required. A fully-qualified model resource name or model ID. Example: "projects/123/locations/us-central1/models/456" or "456" when project and location are initialized or passed. May optionally contain a version ID or alias in {model_name}@{version} form. Or an instance of aiplatform.Model. |
`instances_format` |
`str`
Required. The format in which instances are provided. Must be one of the formats listed in |
`predictions_format` |
`str`
Required. The format in which Vertex AI outputs the predictions, must be one of the formats specified in |
`gcs_source` |
`Optional[Sequence[str]]`
Google Cloud Storage URI(-s) to your instances to run batch prediction on. They must match |
`bigquery_source` |
`Optional[str]`
BigQuery URI to a table, up to 2000 characters long. For example: |
`gcs_destination_prefix` |
`Optional[str]`
The Google Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is |
`bigquery_destination_prefix` |
`Optional[str]`
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name |
`model_parameters` |
`Optional[Dict]`
The parameters that govern the predictions. The schema of the parameters may be specified via the Model's |
`machine_type` |
`Optional[str]`
The type of machine for running batch prediction on dedicated resources. Not specifying machine type will result in batch prediction job being run with automatic resources. |
`accelerator_type` |
`Optional[str]`
The type of accelerator(s) that may be attached to the machine as per |
`accelerator_count` |
`Optional[int]`
The number of accelerators to attach to the |
`starting_replica_count` |
`Optional[int]`
The number of machine replicas used at the start of the batch operation. If not set, Vertex AI decides starting number, not greater than |
`max_replica_count` |
`Optional[int]`
The maximum number of machine replicas the batch operation may be scaled to. Only used if |
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
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`Optional[auth_credentials.Credentials]`
Custom credentials to use to create this batch prediction job. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`batch_size` |
`int`
Optional. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |
`model_monitoring_objective_config` |
`aiplatform.model_monitoring.ObjectiveConfig`
Optional. The objective config for model monitoring. Passing this parameter enables monitoring on the model associated with this batch prediction job. |
`model_monitoring_alert_config` |
`aiplatform.model_monitoring.EmailAlertConfig`
Optional. Configures how model monitoring alerts are sent to the user. Right now only email alert is supported. |
`analysis_instance_schema_uri` |
`str`
Optional. Only applicable if model_monitoring_objective_config is also passed. This parameter specifies the YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |

Returns |
|
|---|---|
Type |
Description |
`(jobs.BatchPredictionJob)` |
Instantiated representation of the created batch prediction job. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### iter_outputs

```
iter_outputs(
bq_max_results: typing.Optional[int] = 100,
) -> typing.Union[
typing.Iterable[storage.Blob], typing.Iterable[bigquery.table.RowIterator]
]
```


Returns an Iterable object to traverse the output files, either a list of GCS Blobs or a BigQuery RowIterator depending on the output config set when the BatchPredictionJob was created.

Parameter |
|
|---|---|
Name |
Description |
`bq_max_results` |
`typing.Optional[int]`
Optional[int] = 100 Limit on rows to retrieve from prediction table in BigQuery dataset. Only used when retrieving predictions from a bigquery_destination_prefix. Default is 100. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If BatchPredictionJob is in a JobState other than SUCCEEDED, since outputs cannot be retrieved until the Job has finished. |
`NotImplementedError` |
If BatchPredictionJob succeeded and output_info does not have a GCS or BQ output provided. |

Returns |
|
|---|---|
Type |
Description |
`Union[Iterable[storage.Blob], Iterable[bigquery.table.RowIterator]]` |
Either a list of GCS Blob objects within the prediction output directory or an iterable BigQuery RowIterator with predictions. |

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

### submit

```
submit(
*,
job_display_name: typing.Optional[str] = None,
model_name: typing.Union[str, google.cloud.aiplatform.models.Model],
instances_format: str = "jsonl",
predictions_format: str = "jsonl",
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bigquery_source: typing.Optional[str] = None,
gcs_destination_prefix: typing.Optional[str] = None,
bigquery_destination_prefix: typing.Optional[str] = None,
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
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
batch_size: typing.Optional[int] = None,
model_monitoring_objective_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
] = None,
model_monitoring_alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.AlertConfig
] = None,
analysis_instance_schema_uri: typing.Optional[str] = None,
service_account: typing.Optional[str] = None
) -> google.cloud.aiplatform.jobs.BatchPredictionJob
```


Sumbit a batch prediction job (not waiting for completion).

Parameters |
|
|---|---|
Name |
Description |
`job_display_name` |
`str`
Required. The user-defined name of the BatchPredictionJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`model_name` |
`Union[str, aiplatform.Model]`
Required. A fully-qualified model resource name or model ID. Example: "projects/123/locations/us-central1/models/456" or "456" when project and location are initialized or passed. May optionally contain a version ID or alias in {model_name}@{version} form. Or an instance of aiplatform.Model. |
`instances_format` |
`str`
Required. The format in which instances are provided. Must be one of the formats listed in |
`predictions_format` |
`str`
Required. The format in which Vertex AI outputs the predictions, must be one of the formats specified in |
`gcs_source` |
`Optional[Sequence[str]]`
Google Cloud Storage URI(-s) to your instances to run batch prediction on. They must match |
`bigquery_source` |
`Optional[str]`
BigQuery URI to a table, up to 2000 characters long. For example: |
`gcs_destination_prefix` |
`Optional[str]`
The Google Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is |
`bigquery_destination_prefix` |
`Optional[str]`
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name |
`model_parameters` |
`Optional[Dict]`
The parameters that govern the predictions. The schema of the parameters may be specified via the Model's |
`machine_type` |
`Optional[str]`
The type of machine for running batch prediction on dedicated resources. Not specifying machine type will result in batch prediction job being run with automatic resources. |
`accelerator_type` |
`Optional[str]`
The type of accelerator(s) that may be attached to the machine as per |
`accelerator_count` |
`Optional[int]`
The number of accelerators to attach to the |
`starting_replica_count` |
`Optional[int]`
The number of machine replicas used at the start of the batch operation. If not set, Vertex AI decides starting number, not greater than |
`max_replica_count` |
`Optional[int]`
The maximum number of machine replicas the batch operation may be scaled to. Only used if |
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
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`Optional[auth_credentials.Credentials]`
Custom credentials to use to create this batch prediction job. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`batch_size` |
`int`
Optional. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |
`model_monitoring_objective_config` |
`aiplatform.model_monitoring.ObjectiveConfig`
Optional. The objective config for model monitoring. Passing this parameter enables monitoring on the model associated with this batch prediction job. |
`model_monitoring_alert_config` |
`aiplatform.model_monitoring.EmailAlertConfig`
Optional. Configures how model monitoring alerts are sent to the user. Right now only email alert is supported. |
`analysis_instance_schema_uri` |
`str`
Optional. Only applicable if model_monitoring_objective_config is also passed. This parameter specifies the YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |

Returns |
|
|---|---|
Type |
Description |
`(jobs.BatchPredictionJob)` |
Instantiated representation of the created batch prediction job. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_serviceindexserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient -->

# Class IndexServiceClient (1.134.0)

```
IndexServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
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
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
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
google.cloud.aiplatform_v1.types.index_service.CreateIndexRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
index: typing.Optional[google.cloud.aiplatform_v1.types.index.Index] = None,
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
from google.cloud import aiplatform_v1
def sample_create_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
index = aiplatform_v1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1.[CreateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexRequest.html)(
parent="parent_value",
index=index,
)
# Make the request
operation = client.[create_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_create_index)(request=request)
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
google.cloud.aiplatform_v1.types.index_service.DeleteIndexRequest, dict
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
from google.cloud import aiplatform_v1
def sample_delete_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_delete_index)(request=request)
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
google.cloud.aiplatform_v1.types.index_service.GetIndexRequest, dict
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
) -> google.cloud.aiplatform_v1.types.index.Index
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
from google.cloud import aiplatform_v1
def sample_get_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_get_index)(request=request)
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
google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest, dict
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
) -> google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesPager
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
from google.cloud import aiplatform_v1
def sample_list_indexes():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListIndexesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_indexes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_list_indexes)(request=request)
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
google.cloud.aiplatform_v1.types.index_service.RemoveDatapointsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.index_service.RemoveDatapointsResponse
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
from google.cloud import aiplatform_v1
def sample_remove_datapoints():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RemoveDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = client.[remove_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_remove_datapoints)(request=request)
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
google.cloud.aiplatform_v1.types.index_service.UpdateIndexRequest, dict
]
] = None,
*,
index: typing.Optional[google.cloud.aiplatform_v1.types.index.Index] = None,
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
from google.cloud import aiplatform_v1
def sample_update_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
index = aiplatform_v1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1.[UpdateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexRequest.html)(
index=index,
)
# Make the request
operation = client.[update_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_update_index)(request=request)
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
google.cloud.aiplatform_v1.types.index_service.UpsertDatapointsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.index_service.UpsertDatapointsResponse
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
from google.cloud import aiplatform_v1
def sample_upsert_datapoints():
# Create a client
client = aiplatform_v1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpsertDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpsertDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = client.[upsert_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceClient_upsert_datapoints)(request=request)
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
