---
merged_at: 2026-01-25T21:47:44.338830
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicejobserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient -->

# Class JobServiceClient (1.134.0)

```
JobServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.job_service.transports.base.JobServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.job_service.transports.base.JobServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's jobs.

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
`JobServiceTransport` |
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

### JobServiceClient

```
JobServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.job_service.transports.base.JobServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.job_service.transports.base.JobServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the job service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,JobServiceTransport,Callable[..., JobServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the JobServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_prediction_job_path

```
batch_prediction_job_path(
project: str, location: str, batch_prediction_job: str
) -> str
```


Returns a fully-qualified batch_prediction_job string.

### cancel_batch_prediction_job

```
cancel_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CancelBatchPredictionJobRequest,
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


Cancels a BatchPredictionJob.

Starts asynchronous cancellation on the BatchPredictionJob. The
server makes the best effort to cancel the job, but success is
not guaranteed. Clients can use
xref_JobService.GetBatchPredictionJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On a successful
cancellation, the BatchPredictionJob is not deleted;instead its
xref_BatchPredictionJob.state
is set to `CANCELLED`

. Any files already outputted by the job
are not deleted.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_cancel_batch_prediction_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelBatchPredictionJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_cancel_batch_prediction_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelBatchPredictionJob. |
`name` |
`str`
Required. The name of the BatchPredictionJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_custom_job

```
cancel_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CancelCustomJobRequest,
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


Cancels a CustomJob. Starts asynchronous cancellation on the
CustomJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_JobService.GetCustomJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the CustomJob is not deleted; instead it becomes a
job with a
xref_CustomJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_CustomJob.state
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
def sample_cancel_custom_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelCustomJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_cancel_custom_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelCustomJob. |
`name` |
`str`
Required. The name of the CustomJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_data_labeling_job

```
cancel_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CancelDataLabelingJobRequest,
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


Cancels a DataLabelingJob. Success of cancellation is not guaranteed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_cancel_data_labeling_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelDataLabelingJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_cancel_data_labeling_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelDataLabelingJob. |
`name` |
`str`
Required. The name of the DataLabelingJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_hyperparameter_tuning_job

```
cancel_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CancelHyperparameterTuningJobRequest,
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


Cancels a HyperparameterTuningJob. Starts asynchronous
cancellation on the HyperparameterTuningJob. The server makes a
best effort to cancel the job, but success is not guaranteed.
Clients can use
xref_JobService.GetHyperparameterTuningJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the HyperparameterTuningJob is not deleted;
instead it becomes a job with a
xref_HyperparameterTuningJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_HyperparameterTuningJob.state
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
def sample_cancel_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelHyperparameterTuningJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_cancel_hyperparameter_tuning_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelHyperparameterTuningJob. |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### cancel_nas_job

```
cancel_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CancelNasJobRequest, dict
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


Cancels a NasJob. Starts asynchronous cancellation on the
NasJob. The server makes a best effort to cancel the job, but
success is not guaranteed. Clients can use
xref_JobService.GetNasJob
or other methods to check whether the cancellation succeeded or
whether the job completed despite cancellation. On successful
cancellation, the NasJob is not deleted; instead it becomes a
job with a
xref_NasJob.error
value with a `google.rpc.Status.code][google.rpc.Status.code]`

of
1, corresponding to `Code.CANCELLED`

, and
xref_NasJob.state is
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
from google.cloud import aiplatform_v1beta1
def sample_cancel_nas_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CancelNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelNasJobRequest.html)(
name="name_value",
)
# Make the request
client.[cancel_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_cancel_nas_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CancelNasJob. |
`name` |
`str`
Required. The name of the NasJob to cancel. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_batch_prediction_job

```
create_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CreateBatchPredictionJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
batch_prediction_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.batch_prediction_job.BatchPredictionJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.batch_prediction_job.BatchPredictionJob
```


Creates a BatchPredictionJob. A BatchPredictionJob once created will right away be attempted to start.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_batch_prediction_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
batch_prediction_job = aiplatform_v1beta1.[BatchPredictionJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.html)()
batch_prediction_job.display_name = "display_name_value"
batch_prediction_job.input_config.gcs_source.uris = ['uris_value1', 'uris_value2']
batch_prediction_job.input_config.instances_format = "instances_format_value"
batch_prediction_job.output_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
batch_prediction_job.output_config.predictions_format = "predictions_format_value"
request = aiplatform_v1beta1.[CreateBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateBatchPredictionJobRequest.html)(
parent="parent_value",
batch_prediction_job=batch_prediction_job,
)
# Make the request
response = client.[create_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_create_batch_prediction_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateBatchPredictionJob. |
`parent` |
`str`
Required. The resource name of the Location to create the BatchPredictionJob in. Format: |
`batch_prediction_job` |
Required. The BatchPredictionJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances. |

### create_custom_job

```
create_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CreateCustomJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
custom_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.custom_job.CustomJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.custom_job.CustomJob
```


Creates a CustomJob. A created CustomJob right away will be attempted to be run.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_custom_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
custom_job = aiplatform_v1beta1.[CustomJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob.html)()
custom_job.display_name = "display_name_value"
custom_job.job_spec.worker_pool_specs.container_spec.image_uri = "image_uri_value"
request = aiplatform_v1beta1.[CreateCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateCustomJobRequest.html)(
parent="parent_value",
custom_job=custom_job,
)
# Make the request
response = client.[create_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_create_custom_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateCustomJob. |
`parent` |
`str`
Required. The resource name of the Location to create the CustomJob in. Format: |
`custom_job` |
Required. The CustomJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded). |

### create_data_labeling_job

```
create_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CreateDataLabelingJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
data_labeling_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.data_labeling_job.DataLabelingJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.data_labeling_job.DataLabelingJob
```


Creates a DataLabelingJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_data_labeling_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
data_labeling_job = aiplatform_v1beta1.[DataLabelingJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob.html)()
data_labeling_job.display_name = "display_name_value"
data_labeling_job.datasets = ['datasets_value1', 'datasets_value2']
data_labeling_job.labeler_count = 1375
data_labeling_job.instruction_uri = "instruction_uri_value"
data_labeling_job.inputs_schema_uri = "inputs_schema_uri_value"
data_labeling_job.inputs.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDataLabelingJobRequest.html)(
parent="parent_value",
data_labeling_job=data_labeling_job,
)
# Make the request
response = client.[create_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_create_data_labeling_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateDataLabelingJob. |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: |
`data_labeling_job` |
Required. The DataLabelingJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset: |

### create_hyperparameter_tuning_job

```
create_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CreateHyperparameterTuningJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
hyperparameter_tuning_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.hyperparameter_tuning_job.HyperparameterTuningJob
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
google.cloud.aiplatform_v1beta1.types.hyperparameter_tuning_job.HyperparameterTuningJob
)
```


Creates a HyperparameterTuningJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
hyperparameter_tuning_job = aiplatform_v1beta1.[HyperparameterTuningJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HyperparameterTuningJob.html)()
hyperparameter_tuning_job.display_name = "display_name_value"
hyperparameter_tuning_job.study_spec.metrics.metric_id = "metric_id_value"
hyperparameter_tuning_job.study_spec.metrics.goal = "MINIMIZE"
hyperparameter_tuning_job.study_spec.parameters.double_value_spec.min_value = 0.96
hyperparameter_tuning_job.study_spec.parameters.double_value_spec.max_value = 0.962
hyperparameter_tuning_job.study_spec.parameters.parameter_id = "parameter_id_value"
hyperparameter_tuning_job.max_trial_count = 1609
hyperparameter_tuning_job.parallel_trial_count = 2128
hyperparameter_tuning_job.trial_job_spec.worker_pool_specs.container_spec.image_uri = "image_uri_value"
request = aiplatform_v1beta1.[CreateHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateHyperparameterTuningJobRequest.html)(
parent="parent_value",
hyperparameter_tuning_job=hyperparameter_tuning_job,
)
# Make the request
response = client.[create_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_create_hyperparameter_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateHyperparameterTuningJob. |
`parent` |
`str`
Required. The resource name of the Location to create the HyperparameterTuningJob in. Format: |
`hyperparameter_tuning_job` |
Required. The HyperparameterTuningJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification. |

### create_model_deployment_monitoring_job

```
create_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CreateModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_deployment_monitoring_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
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
google.cloud.aiplatform_v1beta1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
)
```


Creates a ModelDeploymentMonitoringJob. It will run periodically on a configured interval.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
model_deployment_monitoring_job = aiplatform_v1beta1.[ModelDeploymentMonitoringJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob.html)()
model_deployment_monitoring_job.display_name = "display_name_value"
model_deployment_monitoring_job.endpoint = "endpoint_value"
request = aiplatform_v1beta1.[CreateModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelDeploymentMonitoringJobRequest.html)(
parent="parent_value",
model_deployment_monitoring_job=model_deployment_monitoring_job,
)
# Make the request
response = client.[create_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_create_model_deployment_monitoring_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateModelDeploymentMonitoringJob. |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: |
`model_deployment_monitoring_job` |
Required. The ModelDeploymentMonitoringJob to create This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors. |

### create_nas_job

```
create_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.CreateNasJobRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
nas_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.nas_job.NasJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.nas_job.NasJob
```


Creates a NasJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_nas_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
nas_job = aiplatform_v1beta1.[NasJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJob.html)()
nas_job.display_name = "display_name_value"
nas_job.nas_job_spec.multi_trial_algorithm_spec.search_trial_spec.search_trial_job_spec.worker_pool_specs.container_spec.image_uri = "image_uri_value"
nas_job.nas_job_spec.multi_trial_algorithm_spec.search_trial_spec.max_trial_count = 1609
nas_job.nas_job_spec.multi_trial_algorithm_spec.search_trial_spec.max_parallel_trial_count = 2549
request = aiplatform_v1beta1.[CreateNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNasJobRequest.html)(
parent="parent_value",
nas_job=nas_job,
)
# Make the request
response = client.[create_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_create_nas_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.CreateNasJob. |
`parent` |
`str`
Required. The resource name of the Location to create the NasJob in. Format: |
`nas_job` |
Required. The NasJob to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a Neural Architecture Search (NAS) job. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

### data_labeling_job_path

`data_labeling_job_path(project: str, location: str, data_labeling_job: str) -> str`


Returns a fully-qualified data_labeling_job string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

### delete_batch_prediction_job

```
delete_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.DeleteBatchPredictionJobRequest,
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


Deletes a BatchPredictionJob. Can only be called on jobs that already finished.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_batch_prediction_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteBatchPredictionJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_delete_batch_prediction_job)(request=request)
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
The request object. Request message for JobService.DeleteBatchPredictionJob. |
`name` |
`str`
Required. The name of the BatchPredictionJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_custom_job

```
delete_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.DeleteCustomJobRequest,
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


Deletes a CustomJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_custom_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCustomJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_delete_custom_job)(request=request)
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
The request object. Request message for JobService.DeleteCustomJob. |
`name` |
`str`
Required. The name of the CustomJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_data_labeling_job

```
delete_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.DeleteDataLabelingJobRequest,
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


Deletes a DataLabelingJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_data_labeling_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDataLabelingJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_delete_data_labeling_job)(request=request)
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
The request object. Request message for JobService.DeleteDataLabelingJob. |
`name` |
`str`
Required. The name of the DataLabelingJob to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_hyperparameter_tuning_job

```
delete_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.DeleteHyperparameterTuningJobRequest,
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


Deletes a HyperparameterTuningJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteHyperparameterTuningJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_delete_hyperparameter_tuning_job)(request=request)
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
The request object. Request message for JobService.DeleteHyperparameterTuningJob. |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_model_deployment_monitoring_job

```
delete_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.DeleteModelDeploymentMonitoringJobRequest,
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


Deletes a ModelDeploymentMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_delete_model_deployment_monitoring_job)(request=request)
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
The request object. Request message for JobService.DeleteModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_nas_job

```
delete_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.DeleteNasJobRequest, dict
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


Deletes a NasJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_nas_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNasJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_delete_nas_job)(request=request)
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
The request object. Request message for JobService.DeleteNasJob. |
`name` |
`str`
Required. The name of the NasJob resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`JobServiceClient` |
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
`JobServiceClient` |
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
`JobServiceClient` |
The constructed client. |

### get_batch_prediction_job

```
get_batch_prediction_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetBatchPredictionJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.batch_prediction_job.BatchPredictionJob
```


Gets a BatchPredictionJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_batch_prediction_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetBatchPredictionJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetBatchPredictionJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_batch_prediction_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_batch_prediction_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetBatchPredictionJob. |
`name` |
`str`
Required. The name of the BatchPredictionJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances. |

### get_custom_job

```
get_custom_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetCustomJobRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.types.custom_job.CustomJob
```


Gets a CustomJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_custom_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetCustomJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetCustomJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_custom_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_custom_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetCustomJob. |
`name` |
`str`
Required. The name of the CustomJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded). |

### get_data_labeling_job

```
get_data_labeling_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetDataLabelingJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.data_labeling_job.DataLabelingJob
```


Gets a DataLabelingJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_data_labeling_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDataLabelingJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDataLabelingJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_data_labeling_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_data_labeling_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetDataLabelingJob. |
`name` |
`str`
Required. The name of the DataLabelingJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset: |

### get_hyperparameter_tuning_job

```
get_hyperparameter_tuning_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetHyperparameterTuningJobRequest,
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
google.cloud.aiplatform_v1beta1.types.hyperparameter_tuning_job.HyperparameterTuningJob
)
```


Gets a HyperparameterTuningJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_hyperparameter_tuning_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetHyperparameterTuningJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetHyperparameterTuningJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_hyperparameter_tuning_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_hyperparameter_tuning_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetHyperparameterTuningJob. |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification. |

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

### get_model_deployment_monitoring_job

```
get_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetModelDeploymentMonitoringJobRequest,
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
google.cloud.aiplatform_v1beta1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
)
```


Gets a ModelDeploymentMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_model_deployment_monitoring_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors. |

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

### get_nas_job

```
get_nas_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetNasJobRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.types.nas_job.NasJob
```


Gets a NasJob

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_nas_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNasJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNasJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_nas_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_nas_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetNasJob. |
`name` |
`str`
Required. The name of the NasJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a Neural Architecture Search (NAS) job. |

### get_nas_trial_detail

```
get_nas_trial_detail(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.GetNasTrialDetailRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.nas_job.NasTrialDetail
```


Gets a NasTrialDetail.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_nas_trial_detail():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetNasTrialDetailRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNasTrialDetailRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_nas_trial_detail](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_get_nas_trial_detail)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.GetNasTrialDetail. |
`name` |
`str`
Required. The name of the NasTrialDetail resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned. |

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

### hyperparameter_tuning_job_path

```
hyperparameter_tuning_job_path(
project: str, location: str, hyperparameter_tuning_job: str
) -> str
```


Returns a fully-qualified hyperparameter_tuning_job string.

### list_batch_prediction_jobs

```
list_batch_prediction_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsPager
)
```


Lists BatchPredictionJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_batch_prediction_jobs():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListBatchPredictionJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_batch_prediction_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_batch_prediction_jobs)(request=request)
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
The request object. Request message for JobService.ListBatchPredictionJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the BatchPredictionJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListBatchPredictionJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_custom_jobs

```
list_custom_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsPager
```


Lists CustomJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_custom_jobs():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListCustomJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_custom_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_custom_jobs)(request=request)
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
The request object. Request message for JobService.ListCustomJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the CustomJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListCustomJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_data_labeling_jobs

```
list_data_labeling_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsPager
)
```


Lists DataLabelingJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_data_labeling_jobs():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDataLabelingJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_data_labeling_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_data_labeling_jobs)(request=request)
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
The request object. Request message for JobService.ListDataLabelingJobs. |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListDataLabelingJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_hyperparameter_tuning_jobs

```
list_hyperparameter_tuning_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsPager
)
```


Lists HyperparameterTuningJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_hyperparameter_tuning_jobs():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListHyperparameterTuningJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_hyperparameter_tuning_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_hyperparameter_tuning_jobs)(request=request)
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
The request object. Request message for JobService.ListHyperparameterTuningJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the HyperparameterTuningJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListHyperparameterTuningJobs Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_model_deployment_monitoring_jobs

```
list_model_deployment_monitoring_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager
)
```


Lists ModelDeploymentMonitoringJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_model_deployment_monitoring_jobs():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelDeploymentMonitoringJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_deployment_monitoring_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_model_deployment_monitoring_jobs)(request=request)
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
The request object. Request message for JobService.ListModelDeploymentMonitoringJobs. |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListModelDeploymentMonitoringJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_nas_jobs

```
list_nas_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsPager
```


Lists NasJobs in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_nas_jobs():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNasJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_nas_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_nas_jobs)(request=request)
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
The request object. Request message for JobService.ListNasJobs. |
`parent` |
`str`
Required. The resource name of the Location to list the NasJobs from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListNasJobs Iterating over this object will yield results and resolve additional pages automatically. |

### list_nas_trial_details

```
list_nas_trial_details(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
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
google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsPager
)
```


List top NasTrialDetails of a NasJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_nas_trial_details():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListNasTrialDetailsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_nas_trial_details](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_list_nas_trial_details)(request=request)
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
The request object. Request message for JobService.ListNasTrialDetails. |
`parent` |
`str`
Required. The name of the NasJob resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.ListNasTrialDetails Iterating over this object will yield results and resolve additional pages automatically. |

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

### nas_job_path

`nas_job_path(project: str, location: str, nas_job: str) -> str`


Returns a fully-qualified nas_job string.

### nas_trial_detail_path

```
nas_trial_detail_path(
project: str, location: str, nas_job: str, nas_trial_detail: str
) -> str
```


Returns a fully-qualified nas_trial_detail string.

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notification_channel_path

`notification_channel_path(project: str, notification_channel: str) -> str`


Returns a fully-qualified notification_channel string.

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

### parse_data_labeling_job_path

`parse_data_labeling_job_path(path: str) -> typing.Dict[str, str]`


Parses a data_labeling_job path into its component segments.

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_hyperparameter_tuning_job_path

`parse_hyperparameter_tuning_job_path(path: str) -> typing.Dict[str, str]`


Parses a hyperparameter_tuning_job path into its component segments.

### parse_model_deployment_monitoring_job_path

`parse_model_deployment_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_deployment_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_nas_job_path

`parse_nas_job_path(path: str) -> typing.Dict[str, str]`


Parses a nas_job path into its component segments.

### parse_nas_trial_detail_path

`parse_nas_trial_detail_path(path: str) -> typing.Dict[str, str]`


Parses a nas_trial_detail path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notification_channel_path

`parse_notification_channel_path(path: str) -> typing.Dict[str, str]`


Parses a notification_channel path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_tensorboard_path

`parse_tensorboard_path(path: str) -> typing.Dict[str, str]`


Parses a tensorboard path into its component segments.

### parse_trial_path

`parse_trial_path(path: str) -> typing.Dict[str, str]`


Parses a trial path into its component segments.

### pause_model_deployment_monitoring_job

```
pause_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.PauseModelDeploymentMonitoringJobRequest,
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


Pauses a ModelDeploymentMonitoringJob. If the job is running, the server makes a best effort to cancel the job. Will mark xref_ModelDeploymentMonitoringJob.state to 'PAUSED'.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_pause_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[PauseModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
client.[pause_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_pause_model_deployment_monitoring_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.PauseModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to pause. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_model_deployment_monitoring_job

```
resume_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.ResumeModelDeploymentMonitoringJobRequest,
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


Resumes a paused ModelDeploymentMonitoringJob. It will start to run from next scheduled time. A deleted ModelDeploymentMonitoringJob can't be resumed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_resume_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ResumeModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeModelDeploymentMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
client.[resume_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_resume_model_deployment_monitoring_job)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for JobService.ResumeModelDeploymentMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to resume. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### search_model_deployment_monitoring_stats_anomalies

```
search_model_deployment_monitoring_stats_anomalies(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
dict,
]
] = None,
*,
model_deployment_monitoring_job: typing.Optional[str] = None,
deployed_model_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager
)
```


Searches Model Monitoring Statistics generated within a given time window.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_model_deployment_monitoring_stats_anomalies():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchModelDeploymentMonitoringStatsAnomaliesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.html)(
model_deployment_monitoring_job="model_deployment_monitoring_job_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
page_result = client.[search_model_deployment_monitoring_stats_anomalies](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_search_model_deployment_monitoring_stats_anomalies)(request=request)
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
The request object. Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies. |
`model_deployment_monitoring_job` |
`str`
Required. ModelDeploymentMonitoring Job resource name. Format: |
`deployed_model_id` |
`str`
Required. The DeployedModel ID of the [ModelDeploymentMonitoringObjectiveConfig.deployed_model_id]. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for JobService.SearchModelDeploymentMonitoringStatsAnomalies. Iterating over this object will yield results and resolve additional pages automatically. |

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

### tensorboard_path

`tensorboard_path(project: str, location: str, tensorboard: str) -> str`


Returns a fully-qualified tensorboard string.

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

### trial_path

`trial_path(project: str, location: str, study: str, trial: str) -> str`


Returns a fully-qualified trial string.

### update_model_deployment_monitoring_job

```
update_model_deployment_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.job_service.UpdateModelDeploymentMonitoringJobRequest,
dict,
]
] = None,
*,
model_deployment_monitoring_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_deployment_monitoring_job.ModelDeploymentMonitoringJob
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


Updates a ModelDeploymentMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_model_deployment_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[JobServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html)()
# Initialize request argument(s)
model_deployment_monitoring_job = aiplatform_v1beta1.[ModelDeploymentMonitoringJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob.html)()
model_deployment_monitoring_job.display_name = "display_name_value"
model_deployment_monitoring_job.endpoint = "endpoint_value"
request = aiplatform_v1beta1.[UpdateModelDeploymentMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobRequest.html)(
model_deployment_monitoring_job=model_deployment_monitoring_job,
)
# Make the request
operation = client.[update_model_deployment_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient.html#google_cloud_aiplatform_v1beta1_services_job_service_JobServiceClient_update_model_deployment_monitoring_job)(request=request)
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
The request object. Request message for JobService.UpdateModelDeploymentMonitoringJob. |
`model_deployment_monitoring_job` |
Required. The model monitoring configuration which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask is used to specify the fields to be overwritten in the ModelDeploymentMonitoringJob resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest_google_877f1b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest_googlec_d65a81.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest_googlecl_c8543c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest_googleclo_4a4cf2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest_googleclou_638640.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest_googlecloud_3678ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexporttensorboardtimeseriesdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataRequest -->

# Class ExportTensorboardTimeSeriesDataRequest (1.134.0)

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to export data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`filter` |
`str`
Exports the TensorboardTimeSeries' data that match the filter expression. |
`page_size` |
`int`
The maximum number of data points to return per page. The default page_size is 1000. Values must be between 1 and 10000. Values above 10000 are coerced to 10000. |
`page_token` |
`str`
A page token, received from a previous ExportTensorboardTimeSeriesData call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to ExportTensorboardTimeSeriesData must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the TensorboardTimeSeries' data. By default, TensorboardTimeSeries' data is returned in a pseudo random order. |

## Methods

### ExportTensorboardTimeSeriesDataRequest

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringstatsdatapointtypedvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsDataPoint.TypedValue -->

# Class TypedValue (1.134.0)

`TypedValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Typed value of the statistics.

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
`double_value` |
`float`
Double. This field is a member of `oneof` _ `value` .
|
`distribution_value` |
Distribution. This field is a member of `oneof` _ `value` .
|

## Classes

### DistributionDataValue

`DistributionDataValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary statistics for a population of values.

## Methods

### TypedValue

`TypedValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Typed value of the statistics.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgeneratesyntheticdatarequest_googlecloudaiplatform_53022b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeneratesyntheticdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataRequest -->

# Class GenerateSyntheticDataRequest (1.134.0)

```
GenerateSyntheticDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DataFoundryService.GenerateSyntheticData.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`task_description` |
Generate data from a high-level task description. This field is a member of `oneof` _ `strategy` .
|
`location` |
`str`
Required. The resource name of the Location to run the job. Format: `projects/{project}/locations/{location}`
|
`count` |
`int`
Required. The number of synthetic examples to generate. For this stateless API, the count is limited to a small number. |
`output_field_specs` |
`MutableSequence[`
Required. The schema of the desired output, defined by a list of fields. |
`examples` |
`MutableSequence[`
Optional. A list of few-shot examples to guide the model's output style and format. |

## Methods

### GenerateSyntheticDataRequest

```
GenerateSyntheticDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DataFoundryService.GenerateSyntheticData.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringstatsdatapoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsDataPoint -->

# Class ModelMonitoringStatsDataPoint (1.134.0)

```
ModelMonitoringStatsDataPoint(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a single statistics data point.

## Attributes |
|
|---|---|
Name |
Description |
`current_stats` |
Statistics from current dataset. |
`baseline_stats` |
Statistics from baseline dataset. |
`threshold_value` |
`float`
Threshold value. |
`has_anomaly` |
`bool`
Indicate if the statistics has anomaly. |
`model_monitoring_job` |
`str`
Model monitoring job resource name. |
`schedule` |
`str`
Schedule resource name. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Statistics create time. |
`algorithm` |
`str`
Algorithm used to calculated the metrics, eg: jensen_shannon_divergence, l_infinity. |

## Classes

### TypedValue

`TypedValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Typed value of the statistics.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ModelMonitoringStatsDataPoint

```
ModelMonitoringStatsDataPoint(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a single statistics data point.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratecontentrequest_googlecloudaiplatform__9f8bcd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratecontentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest -->

# Class GenerateContentRequest (1.134.0)

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`
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
`model_armor_config` |
Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safety_settings must not be supplied. |
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

### GenerateContentRequest

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescustomjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob -->

# Class CustomJob (1.134.0)

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a CustomJob. |
`display_name` |
`str`
Required. The display name of the CustomJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`job_spec` |
Required. Job spec. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |
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

## Methods

### CustomJob

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesmetadatastoremetadatastorestate_googlecloudaipl_cbf2f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmetadatastoremetadatastorestate_googlecloudaipla_4ce9fc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmetadatastoremetadatastorestate_googlecloudaiplat_fd0801.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmetadatastoremetadatastorestate_googlecloudaiplatf_431285.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetadatastoremetadatastorestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataStore.MetadataStoreState -->

# Class MetadataStoreState (1.134.0)

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.

## Attribute |
|
|---|---|
Name |
Description |
`disk_utilization_bytes` |
`int`
The disk utilization of the MetadataStore in bytes. |

## Methods

### MetadataStoreState

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescopymodeloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelOperationMetadata -->

# Class CopyModelOperationMetadata (1.134.0)

`CopyModelOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of ModelService.CopyModel operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### CopyModelOperationMetadata

`CopyModelOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of ModelService.CopyModel operation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesuploadragfileresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileResponse -->

# Class UploadRagFileResponse (1.134.0)

`UploadRagFileResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.UploadRagFile.

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
`rag_file` |
The RagFile that had been uploaded into the RagCorpus. This field is a member of `oneof` _ `result` .
|
`error` |
`google.rpc.status_pb2.Status`
The error that occurred while processing the RagFile. This field is a member of `oneof` _ `result` .
|

## Methods

### UploadRagFileResponse

`UploadRagFileResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.UploadRagFile.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploygke_googlecl_e9cb10.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploygke_googleclo_f39570.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploygke.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.DeployGke -->

# Class DeployGke (1.134.0)

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment

## Attribute |
|
|---|---|
Name |
Description |
`gke_yaml_configs` |
`MutableSequence[str]`
Optional. GKE deployment configuration in yaml format. |

## Methods

### DeployGke

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescorroboratecontentrequestparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest.Parameters -->

# Class Parameters (1.134.0)

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.

## Attribute |
|
|---|---|
Name |
Description |
`citation_threshold` |
`float`
Optional. Only return claims with citation score larger than the threshold. |

## Methods

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeniesource_googlecloudaiplatform_v1beta1type_9ed85c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeniesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenieSource -->

# Class GenieSource (1.134.0)

`GenieSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Generative AI Studio.

## Attribute |
|
|---|---|
Name |
Description |
`base_model_uri` |
`str`
Required. The public base model URI. |

## Methods

### GenieSource

`GenieSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Generative AI Studio.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesblob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Blob -->

# Class Blob (1.134.0)

`Blob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content blob.

It's preferred to send as text directly rather than raw bytes.

## Attributes |
|
|---|---|
Name |
Description |
`mime_type` |
`str`
Required. The IANA standard MIME type of the source data. |
`data` |
`bytes`
Required. Raw bytes. |

## Methods

### Blob

`Blob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content blob.

It's preferred to send as text directly rather than raw bytes.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespairwisesummarizationqualityinstance__googlecloud_96c4df.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespairwisesummarizationqualityinstance__googleclouda_d79e5a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespairwisesummarizationqualityinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseSummarizationQualityInstance -->

# Class PairwiseSummarizationQualityInstance (1.134.0)

```
PairwiseSummarizationQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality instance.

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
Required. Text to be summarized. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Summarization prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### PairwiseSummarizationQualityInstance

```
PairwiseSummarizationQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstoptrialrequest_googlecloudaiplatform_v1type_b349b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstoptrialrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopTrialRequest -->

# Class StopTrialRequest (1.134.0)

`StopTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.StopTrial.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### StopTrialRequest

`StopTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.StopTrial.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteOperationMetadata -->

# Class DeleteOperationMetadata (1.134.0)

`DeleteOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform deletes of any entities.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### DeleteOperationMetadata

`DeleteOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform deletes of any entities.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesreasoning_engine_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.reasoning_engine_service.pagers`

module.

## Classes

[ListReasoningEnginesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager)

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse) object, and
provides an `__aiter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListReasoningEnginesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers.ListReasoningEnginesPager)

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse) object, and
provides an `__iter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__iter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesgettrialrequest_googlecloudaiplatform_v1t_c7e1c7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesgettrialrequest_googlecloudaiplatform_v1ty_76ad10.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesgettrialrequest_googlecloudaiplatform_v1typ_868563.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgettrialrequest_googlecloudaiplatform_v1type_70c8c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgettrialrequest_googlecloudaiplatform_v1types_1e9e79.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgettrialrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTrialRequest -->

# Class GetTrialRequest (1.134.0)

`GetTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetTrial.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Trial resource. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### GetTrialRequest

`GetTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetTrial.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespurgeartifactsmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsMetadata -->

# Class PurgeArtifactsMetadata (1.134.0)

`PurgeArtifactsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeArtifacts.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for purging Artifacts. |

## Methods

### PurgeArtifactsMetadata

`PurgeArtifactsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform MetadataService.PurgeArtifacts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescorroboratecontentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest -->

# Class CorroborateContentRequest (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescustomjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJob -->

# Class CustomJob (1.134.0)

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a CustomJob. |
`display_name` |
`str`
Required. The display name of the CustomJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`job_spec` |
Required. Job spec. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |
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

## Methods

### CustomJob

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexporttensorboardtimeseriesdatarequest__goog_8b399c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexporttensorboardtimeseriesdatarequest__googl_d8f7dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexporttensorboardtimeseriesdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataRequest -->

# Class ExportTensorboardTimeSeriesDataRequest (1.134.0)

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to export data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`filter` |
`str`
Exports the TensorboardTimeSeries' data that match the filter expression. |
`page_size` |
`int`
The maximum number of data points to return per page. The default page_size is 1000. Values must be between 1 and 10000. Values above 10000 are coerced to 10000. |
`page_token` |
`str`
A page token, received from a previous ExportTensorboardTimeSeriesData call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to ExportTensorboardTimeSeriesData must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the TensorboardTimeSeries' data. By default, TensorboardTimeSeries' data is returned in a pseudo random order. |

## Methods

### ExportTensorboardTimeSeriesDataRequest

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfie_d4b1e7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfieldmappingnumericrestrictvaluetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping.NumericRestrict.ValueType -->

# Class ValueType (1.134.0)

`ValueType(value)`


The type of numeric value for the restrict.

## Enums |
|
|---|---|
Name |
Description |
`VALUE_TYPE_UNSPECIFIED` |
Should not be used. |
`INT` |
Represents 64 bit integer. |
`FLOAT` |
Represents 32 bit float. |
`DOUBLE` |
Represents 64 bit float. |

## Methods

### ValueType

`ValueType(value)`


The type of numeric value for the restrict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryrecallspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallSpec -->

# Class TrajectoryRecallSpec (1.134.0)

`TrajectoryRecallSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryRecall metric - returns a float score based on average recall of individual tool calls.

## Methods

### TrajectoryRecallSpec

`TrajectoryRecallSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryRecall metric - returns a float score based on average recall of individual tool calls.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeneratecontentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentRequest -->

# Class GenerateContentRequest (1.134.0)

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`
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
`model_armor_config` |
Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safety_settings must not be supplied. |
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

### GenerateContentRequest

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesindex_googlecloudaiplatform_v1typesprobe____googl_239dc0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesindex_googlecloudaiplatform_v1typesprobe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindex.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index -->

# Class Index (1.134.0)

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Index. |
`display_name` |
`str`
Required. The display name of the Index. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Index. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Index, that is specific to it. Unset if the Index does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
An additional information about the Index; the schema of the metadata can be found in metadata_schema. |
`deployed_indexes` |
`MutableSequence[`
Output only. The pointers to DeployedIndexes created from this Index. An Index can be only deleted if all its DeployedIndexes had been undeployed first. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Indexes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was most recently updated. This also includes any update to the contents of the Index. Note that Operations working on this Index may have their [Operations.metadata.generic_metadata.update_time] [google.cloud.aiplatform.v1.GenericOperationMetadata.update_time] a little after the value of this timestamp, yet that does not mean their results are not already reflected in the Index. Result of any successfully completed Operation on the Index is reflected in it. |
`index_stats` |
Output only. Stats of the index resource. |
`index_update_method` |
Immutable. The update method to use with this Index. If not set, BATCH_UPDATE will be used by default. |
`encryption_spec` |
Immutable. Customer-managed encryption key spec for an Index. If set, this Index and all sub-resources of this Index will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### IndexUpdateMethod

`IndexUpdateMethod(value)`


The update method of an Index.

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

### Index

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprobe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe -->

# Class Probe (1.134.0)

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

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
`exec_` |
ExecAction probes the health of a container by executing a command. This field is a member of `oneof` _ `probe_type` .
|
`http_get` |
HttpGetAction probes the health of a container by sending an HTTP GET request. This field is a member of `oneof` _ `probe_type` .
|
`grpc` |
GrpcAction probes the health of a container by sending a gRPC request. This field is a member of `oneof` _ `probe_type` .
|
`tcp_socket` |
TcpSocketAction probes the health of a container by opening a TCP socket connection. This field is a member of `oneof` _ `probe_type` .
|
`period_seconds` |
`int`
How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Must be less than timeout_seconds. Maps to Kubernetes probe argument 'periodSeconds'. |
`timeout_seconds` |
`int`
Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Must be greater or equal to period_seconds. Maps to Kubernetes probe argument 'timeoutSeconds'. |
`failure_threshold` |
`int`
Number of consecutive failures before the probe is considered failed. Defaults to 3. Minimum value is 1. Maps to Kubernetes probe argument 'failureThreshold'. |
`success_threshold` |
`int`
Number of consecutive successes before the probe is considered successful. Defaults to 1. Minimum value is 1. Maps to Kubernetes probe argument 'successThreshold'. |
`initial_delay_seconds` |
`int`
Number of seconds to wait before starting the probe. Defaults to 0. Minimum value is 0. Maps to Kubernetes probe argument 'initialDelaySeconds'. |

## Classes

### ExecAction

`ExecAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ExecAction specifies a command to execute.

### GrpcAction

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

### HttpGetAction

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.

### HttpHeader

`HttpHeader(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpHeader describes a custom header to be used in HTTP probes

### TcpSocketAction

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

## Methods

### Probe

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeaturevaluelist_googlecloudaiplatform_v1beta1ty_4ac383.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeaturevaluelist_googlecloudaiplatform_v1beta1typ_19bac4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturevaluelist_googlecloudaiplatform_v1beta1type_6ebe76.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturevaluelist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueList -->

# Class FeatureValueList (1.134.0)

`FeatureValueList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container for list of values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[google.cloud.aiplatform_v1.types.FeatureValue]`
A list of feature values. All of them should be the same data type. |

## Methods

### FeatureValueList

`FeatureValueList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container for list of values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesrequestdirectcontentssourceevent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.DirectContentsSource.Event -->

# Class Event (1.134.0)

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single piece of conversation from which to generate memories.

## Attribute |
|
|---|---|
Name |
Description |
`content` |
Required. A single piece of content from which to generate memories. |

## Methods

### Event

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single piece of conversation from which to generate memories.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeaturevaluelist_googlecloudaiplatform_v1beta_572fa7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturevaluelist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueList -->

# Class FeatureValueList (1.134.0)

`FeatureValueList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container for list of values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.FeatureValue]`
A list of feature values. All of them should be the same data type. |

## Methods

### FeatureValueList

`FeatureValueList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container for list of values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryrecallresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallResults -->

# Class TrajectoryRecallResults (1.134.0)

`TrajectoryRecallResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryRecall metric.

## Attribute |
|
|---|---|
Name |
Description |
`trajectory_recall_metric_values` |
`MutableSequence[`
Output only. TrajectoryRecall metric values. |

## Methods

### TrajectoryRecallResults

`TrajectoryRecallResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryRecall metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewvectorsearchconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig -->

# Class VectorSearchConfig (1.134.0)

`VectorSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated. Use IndexConfig instead.

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
`tree_ah_config` |
Optional. Configuration options for the tree-AH algorithm (Shallow tree + Asymmetric Hashing). Please refer to this paper for more details: https://arxiv.org/abs/1908.10396 This field is a member of `oneof` _ `algorithm_config` .
|
`brute_force_config` |
`google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig.BruteForceConfig`
Optional. Configuration options for using brute force search, which simply implements the standard linear search in the database for each query. It is primarily meant for benchmarking and to generate the ground truth for approximate search. This field is a member of `oneof` _ `algorithm_config` .
|
`embedding_column` |
`str`
Optional. Column of embedding. This column contains the source data to create index for vector search. embedding_column must be set when using vector search. |
`filter_columns` |
`MutableSequence[str]`
Optional. Columns of features that're used to filter vector search results. |
`crowding_column` |
`str`
Optional. Column of crowding. This column contains crowding attribute which is a constraint on a neighbor list produced by FeatureOnlineStoreService.SearchNearestEntities to diversify search results. If NearestNeighborQuery.per_crowding_attribute_neighbor_count is set to K in SearchNearestEntitiesRequest, it's guaranteed that no more than K entities of the same crowding attribute are returned in the response. |
`embedding_dimension` |
`int`
Optional. The number of dimensions of the input embedding. This field is a member of `oneof` _ `_embedding_dimension` .
|
`distance_measure_type` |
Optional. The distance measure used in nearest neighbor search. |

## Classes

### DistanceMeasureType

`DistanceMeasureType(value)`


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


### TreeAHConfig

`TreeAHConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### VectorSearchConfig

`VectorSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated. Use IndexConfig instead.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicefeatureonlinestoreadminserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient -->

# Class FeatureOnlineStoreAdminServiceClient (1.134.0)

```
FeatureOnlineStoreAdminServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that handles CRUD and List for resources for FeatureOnlineStore.

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
`FeatureOnlineStoreAdminServiceTransport` |
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

### FeatureOnlineStoreAdminServiceClient

```
FeatureOnlineStoreAdminServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature online store admin service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeatureOnlineStoreAdminServiceTransport,Callable[..., FeatureOnlineStoreAdminServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureOnlineStoreAdminServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_feature_online_store

```
create_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.CreateFeatureOnlineStoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_online_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_online_store.FeatureOnlineStore
] = None,
feature_online_store_id: typing.Optional[str] = None,
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


Creates a new FeatureOnlineStore in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_feature_online_store():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_online_store = aiplatform_v1beta1.[FeatureOnlineStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.html)()
feature_online_store.bigtable.auto_scaling.min_node_count = 1489
feature_online_store.bigtable.auto_scaling.max_node_count = 1491
request = aiplatform_v1beta1.[CreateFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOnlineStoreRequest.html)(
parent="parent_value",
feature_online_store=feature_online_store,
feature_online_store_id="feature_online_store_id_value",
)
# Make the request
operation = client.[create_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_create_feature_online_store)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore. |
`parent` |
`str`
Required. The resource name of the Location to create FeatureOnlineStores. Format: |
`feature_online_store` |
Required. The FeatureOnlineStore to create. This corresponds to the |
`feature_online_store_id` |
`str`
Required. The ID to use for this FeatureOnlineStore, which will become the final component of the FeatureOnlineStore's resource name. This value may be up to 60 characters, and valid characters are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### create_feature_view

```
create_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.CreateFeatureViewRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_view: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_view.FeatureView
] = None,
feature_view_id: typing.Optional[str] = None,
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


Creates a new FeatureView in a given FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_feature_view():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_view = aiplatform_v1beta1.[FeatureView](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.html)()
feature_view.big_query_source.uri = "uri_value"
feature_view.big_query_source.entity_id_columns = ['entity_id_columns_value1', 'entity_id_columns_value2']
request = aiplatform_v1beta1.[CreateFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureViewRequest.html)(
parent="parent_value",
feature_view=feature_view,
feature_view_id="feature_view_id_value",
)
# Make the request
operation = client.[create_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_create_feature_view)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.CreateFeatureView. |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: |
`feature_view` |
Required. The FeatureView to create. This corresponds to the |
`feature_view_id` |
`str`
Required. The ID to use for the FeatureView, which will become the final component of the FeatureView's resource name. This value may be up to 60 characters, and valid characters are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_feature_online_store

```
delete_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.DeleteFeatureOnlineStoreRequest,
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


Deletes a single FeatureOnlineStore. The FeatureOnlineStore must not contain any FeatureViews.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_feature_online_store():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureOnlineStoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_delete_feature_online_store)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore. |
`name` |
`str`
Required. The name of the FeatureOnlineStore to be deleted. Format: |
`force` |
`bool`
If set to true, any FeatureViews and Features for this FeatureOnlineStore will also be deleted. (Otherwise, the request will only work if the FeatureOnlineStore has no FeatureViews.) This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### delete_feature_view

```
delete_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.DeleteFeatureViewRequest,
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


Deletes a single FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_feature_view():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureViewRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_delete_feature_view)(request=request)
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
The request object. Request message for [FeatureOnlineStoreAdminService.DeleteFeatureViews][]. |
`name` |
`str`
Required. The name of the FeatureView to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### feature_online_store_path

```
feature_online_store_path(
project: str, location: str, feature_online_store: str
) -> str
```


Returns a fully-qualified feature_online_store string.

### feature_view_path

```
feature_view_path(
project: str, location: str, feature_online_store: str, feature_view: str
) -> str
```


Returns a fully-qualified feature_view string.

### feature_view_sync_path

```
feature_view_sync_path(
project: str, location: str, feature_online_store: str, feature_view: str
) -> str
```


Returns a fully-qualified feature_view_sync string.

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
`FeatureOnlineStoreAdminServiceClient` |
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
`FeatureOnlineStoreAdminServiceClient` |
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
`FeatureOnlineStoreAdminServiceClient` |
The constructed client. |

### get_feature_online_store

```
get_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.GetFeatureOnlineStoreRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_online_store.FeatureOnlineStore
```


Gets details of a single FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_feature_online_store():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureOnlineStoreRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_get_feature_online_store)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.GetFeatureOnlineStore. |
`name` |
`str`
Required. The name of the FeatureOnlineStore resource. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container. |

### get_feature_view

```
get_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.GetFeatureViewRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_view.FeatureView
```


Gets details of a single FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_feature_view():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_get_feature_view)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.GetFeatureView. |
`name` |
`str`
Required. The name of the FeatureView resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig. |

### get_feature_view_sync

```
get_feature_view_sync(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.GetFeatureViewSyncRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_view_sync.FeatureViewSync
```


Gets details of a single FeatureViewSync.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_feature_view_sync():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureViewSyncRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewSyncRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_view_sync](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_get_feature_view_sync)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync. |
`name` |
`str`
Required. The name of the FeatureViewSync resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store. |

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

### list_feature_online_stores

```
list_feature_online_stores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager
)
```


Lists FeatureOnlineStores in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_feature_online_stores():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureOnlineStoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_online_stores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_list_feature_online_stores)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores. |
`parent` |
`str`
Required. The resource name of the Location to list FeatureOnlineStores. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_view_syncs

```
list_feature_view_syncs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager
)
```


Lists FeatureViewSyncs in a given FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_feature_view_syncs():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureViewSyncsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_view_syncs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_list_feature_view_syncs)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs. |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_views

```
list_feature_views(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager
)
```


Lists FeatureViews in a given FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_feature_views():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureViewsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_views](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_list_feature_views)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.ListFeatureViews. |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to list FeatureViews. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreAdminService.ListFeatureViews. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_feature_online_store_path

`parse_feature_online_store_path(path: str) -> typing.Dict[str, str]`


Parses a feature_online_store path into its component segments.

### parse_feature_view_path

`parse_feature_view_path(path: str) -> typing.Dict[str, str]`


Parses a feature_view path into its component segments.

### parse_feature_view_sync_path

`parse_feature_view_sync_path(path: str) -> typing.Dict[str, str]`


Parses a feature_view_sync path into its component segments.

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

### sync_feature_view

```
sync_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.SyncFeatureViewRequest,
dict,
]
] = None,
*,
feature_view: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.SyncFeatureViewResponse
)
```


Triggers on-demand sync for the FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_sync_feature_view():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SyncFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SyncFeatureViewRequest.html)(
feature_view="feature_view_value",
)
# Make the request
response = client.[sync_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_sync_feature_view)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.SyncFeatureView. |
`feature_view` |
`str`
Required. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreAdminService.SyncFeatureView. |

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

### update_feature_online_store

```
update_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.UpdateFeatureOnlineStoreRequest,
dict,
]
] = None,
*,
feature_online_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_online_store.FeatureOnlineStore
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


Updates the parameters of a single FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_feature_online_store():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_online_store = aiplatform_v1beta1.[FeatureOnlineStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.html)()
feature_online_store.bigtable.auto_scaling.min_node_count = 1489
feature_online_store.bigtable.auto_scaling.max_node_count = 1491
request = aiplatform_v1beta1.[UpdateFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureOnlineStoreRequest.html)(
feature_online_store=feature_online_store,
)
# Make the request
operation = client.[update_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_update_feature_online_store)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore. |
`feature_online_store` |
Required. The FeatureOnlineStore's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureOnlineStore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### update_feature_view

```
update_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.UpdateFeatureViewRequest,
dict,
]
] = None,
*,
feature_view: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_view.FeatureView
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


Updates the parameters of a single FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_feature_view():
# Create a client
client = aiplatform_v1beta1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_view = aiplatform_v1beta1.[FeatureView](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.html)()
feature_view.big_query_source.uri = "uri_value"
feature_view.big_query_source.entity_id_columns = ['entity_id_columns_value1', 'entity_id_columns_value2']
request = aiplatform_v1beta1.[UpdateFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureViewRequest.html)(
feature_view=feature_view,
)
# Make the request
operation = client.[update_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_update_feature_view)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.UpdateFeatureView. |
`feature_view` |
Required. The FeatureView's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureView resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
