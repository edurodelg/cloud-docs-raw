---
merged_at: 2026-01-25T21:47:44.387933
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesexecution_googlecloudaiplatform_v1beta1servic_37b092.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesexecution_googlecloudaiplatform_v1beta1service_e8b30c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesexecution_googlecloudaiplatform_v1beta1services_014349.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesexecution_googlecloudaiplatform_v1beta1servicesg_83695b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexecution_googlecloudaiplatform_v1beta1servicesge_1d0168.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexecution_googlecloudaiplatform_v1beta1servicesgen_000406.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexecution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Execution -->

# Class Execution (1.134.0)

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Execution. |
`display_name` |
`str`
User provided display name of the Execution. May be up to 128 Unicode characters. |
`state` |
The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines) and the system does not prescribe or check the validity of state transitions. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Executions. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was last updated. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in `schema_title` to use.
Schema title and version is expected to be registered in
earlier Create Schema calls. And both are used together as
unique identifiers to identify schemas within the local
metadata store.
|
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Execution |

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

### State

`State(value)`


Describes the state of the Execution.

## Methods

### Execution

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_cache_servicepagerslistcachedcontentspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsPager -->

# Class ListCachedContentsPager (1.134.0)

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse) object, and
provides an `__iter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCachedContentsPager

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob -->

# Class ModelDeploymentMonitoringJob (1.134.0)

```
ModelDeploymentMonitoringJob(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a ModelDeploymentMonitoringJob. |
`display_name` |
`str`
Required. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob. |
`endpoint` |
`str`
Required. Endpoint resource name. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`state` |
Output only. The detailed state of the monitoring job. When the job is still creating, the state will be 'PENDING'. Once the job is successfully created, the state will be 'RUNNING'. Pause the job, the state will be 'PAUSED'. Resume the job, the state will return to 'RUNNING'. |
`schedule_state` |
Output only. Schedule state when the monitoring job is in Running state. |
`latest_monitoring_pipeline_metadata` |
Output only. Latest triggered monitoring pipeline metadata. |
`model_deployment_monitoring_objective_configs` |
`MutableSequence[`
Required. The config for monitoring objectives. This is a per DeployedModel config. Each DeployedModel needs to be configured separately. |
`model_deployment_monitoring_schedule_config` |
Required. Schedule config for running the monitoring job. |
`logging_sampling_strategy` |
Required. Sample Strategy for logging. |
`model_monitoring_alert_config` |
Alert config for model monitoring. |
`predict_instance_schema_uri` |
`str`
YAML schema file uri describing the format of a single instance, which are given to format this Endpoint's prediction (and explanation). If not set, we will generate predict schema from collected predict requests. |
`sample_predict_instance` |
`google.protobuf.struct_pb2.Value`
Sample Predict instance, same format as PredictRequest.instances, this can be set as a replacement of ModelDeploymentMonitoringJob.predict_instance_schema_uri. If not set, we will generate predict schema from collected predict requests. |
`analysis_instance_schema_uri` |
`str`
YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format(data type) as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`bigquery_tables` |
`MutableSequence[`
Output only. The created bigquery tables for the job under customer project. Customer could do their own query & analysis. There could be 4 log tables in maximum: 1. Training data logging predict request/response 2. Serving data logging predict request/response |
`log_ttl` |
`google.protobuf.duration_pb2.Duration`
The TTL of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your ModelDeploymentMonitoringJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelDeploymentMonitoringJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelDeploymentMonitoringJob was updated most recently. |
`next_schedule_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this monitoring pipeline will be scheduled to run for the next round. |
`stats_anomalies_base_directory` |
Stats anomalies base folder path. |
`encryption_spec` |
Customer-managed encryption key spec for a ModelDeploymentMonitoringJob. If set, this ModelDeploymentMonitoringJob and all sub-resources of this ModelDeploymentMonitoringJob will be secured by this key. |
`enable_monitoring_pipeline_logs` |
`bool`
If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to `Cloud Logging pricing |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
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

### LatestMonitoringPipelineMetadata

```
LatestMonitoringPipelineMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


All metadata of most recent monitoring pipelines.

### MonitoringScheduleState

`MonitoringScheduleState(value)`


The state to Specify the monitoring pipeline.

## Methods

### ModelDeploymentMonitoringJob

```
ModelDeploymentMonitoringJob(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagerslisttuningjobsasync_fe5588.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagerslisttuningjobsasyncp_80c186.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_tuning_servicepagerslisttuningjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager -->

# Class ListTuningJobsAsyncPager (1.134.0)

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

## Methods

### ListTuningJobsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistsavedqueriesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListSavedQueriesAsyncPager -->

# Class ListSavedQueriesAsyncPager (1.134.0)

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

## Methods

### ListSavedQueriesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistmetadatastorespa_ae57a9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistmetadatastorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataStoresPager -->

# Class ListMetadataStoresPager (1.134.0)

```
ListMetadataStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
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


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataStoresPager

```
ListMetadataStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchreadtensorboardtimeseriesdatarequest_googlecl_36cfae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchreadtensorboardtimeseriesdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadTensorboardTimeSeriesDataRequest -->

# Class BatchReadTensorboardTimeSeriesDataRequest (1.134.0)

```
BatchReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard` |
`str`
Required. The resource name of the Tensorboard containing TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}` .
The TensorboardTimeSeries referenced by
time_series
must be sub resources of this Tensorboard.
|
`time_series` |
`MutableSequence[str]`
Required. The resource names of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### BatchReadTensorboardTimeSeriesDataRequest

```
BatchReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesvideoactionrecognitionpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoActionRecognitionPredictionParams -->

# Class VideoActionRecognitionPredictionParams (1.134.0)

```
VideoActionRecognitionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Action Recognition.

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

## Methods

### VideoActionRecognitionPredictionParams

```
VideoActionRecognitionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Action Recognition.

### VideoActionRecognitionPredictionParams

```
VideoActionRecognitionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Action Recognition.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistmetadataschemasrequest_googlecloudaipl_7266e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistmetadataschemasrequest_googlecloudaipla_63fcce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistmetadataschemasrequest_googlecloudaiplat_b10ae7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmetadataschemasrequest_googlecloudaiplatf_166714.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmetadataschemasrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasRequest -->

# Class ListMetadataSchemasRequest (1.134.0)

`ListMetadataSchemasRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataSchemas.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose MetadataSchemas should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of MetadataSchemas to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListMetadataSchemas call. Provide this to retrieve the next page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |
`filter` |
`str`
A query to filter available MetadataSchemas for matching results. |

## Methods

### ListMetadataSchemasRequest

`ListMetadataSchemasRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataSchemas.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragchunk.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagChunk -->

# Class RagChunk (1.134.0)

`RagChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`text` |
`str`
The content of the chunk. |
`page_span` |
If populated, represents where the chunk starts and ends in the document. This field is a member of `oneof` _ `_page_span` .
|

## Classes

### PageSpan

`PageSpan(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents where the chunk starts and ends in the document.

## Methods

### RagChunk

`RagChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespipeline_servicepagerslistpipelinejobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager -->

# Class ListPipelineJobsAsyncPager (1.134.0)

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

## Methods

### ListPipelineJobsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesjobstate_googlecloudaiplatform_v1typescreateartif_804554.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesjobstate_googlecloudaiplatform_v1typescreateartifa_e3020a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesjobstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.JobState -->

# Class JobState (1.134.0)

`JobState(value)`


Describes the state of a job.

## Enums |
|
|---|---|
Name |
Description |
`JOB_STATE_UNSPECIFIED` |
The job state is unspecified. |
`JOB_STATE_QUEUED` |
The job has been just created or resumed and processing has not yet begun. |
`JOB_STATE_PENDING` |
The service is preparing to run the job. |
`JOB_STATE_RUNNING` |
The job is in progress. |
`JOB_STATE_SUCCEEDED` |
The job completed successfully. |
`JOB_STATE_FAILED` |
The job failed. |
`JOB_STATE_CANCELLING` |
The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED`, `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED`. |
`JOB_STATE_CANCELLED` |
The job has been cancelled. |
`JOB_STATE_PAUSED` |
The job has been stopped, and can be resumed. |
`JOB_STATE_EXPIRED` |
The job has expired. |
`JOB_STATE_UPDATING` |
The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state. |
`JOB_STATE_PARTIALLY_SUCCEEDED` |
The job is partially succeeded, some results may be missing due to errors. |

## Methods

### JobState

`JobState(value)`


Describes the state of a job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateArtifactRequest -->

# Class CreateArtifactRequest (1.134.0)

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Artifact should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`artifact` |
Required. The Artifact to create. |
`artifact_id` |
`str`
The {artifact} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
If not provided, the Artifact's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Artifacts in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Artifact.)
|

## Methods

### CreateArtifactRequest

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespipeline_servicepagerslisttrainingpipelinespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager -->

# Class ListTrainingPipelinesPager (1.134.0)

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

## Methods

### ListTrainingPipelinesPager

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupsertexamplesresponse_googlecloudaiplatfor_624951.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupsertexamplesresponse_googlecloudaiplatform_15b032.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupsertexamplesresponse_googlecloudaiplatform__a1b666.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupsertexamplesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesResponse -->

# Class UpsertExamplesResponse (1.134.0)

`UpsertExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.UpsertExamples.

## Attribute |
|
|---|---|
Name |
Description |
`results` |
`MutableSequence[`
A list of results for creating/updating. It's either a successfully created/updated example or a status with an error message. |

## Classes

### UpsertResult

`UpsertResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result for creating/updating a single example.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### UpsertExamplesResponse

`UpsertExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.UpsertExamples.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesacceleratortype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceleratorType -->

# Class AcceleratorType (1.134.0)

`AcceleratorType(value)`


Represents a hardware accelerator type.

## Enums |
|
|---|---|
Name |
Description |
`ACCELERATOR_TYPE_UNSPECIFIED` |
Unspecified accelerator type, which means no accelerator. |
`NVIDIA_TESLA_K80` |
Deprecated: Nvidia Tesla K80 GPU has reached end of support, see https://cloud.google.com/compute/docs/eol/k80-eol. |
`NVIDIA_TESLA_P100` |
Nvidia Tesla P100 GPU. |
`NVIDIA_TESLA_V100` |
Nvidia Tesla V100 GPU. |
`NVIDIA_TESLA_P4` |
Nvidia Tesla P4 GPU. |
`NVIDIA_TESLA_T4` |
Nvidia Tesla T4 GPU. |
`NVIDIA_TESLA_A100` |
Nvidia Tesla A100 GPU. |
`NVIDIA_A100_80GB` |
Nvidia A100 80GB GPU. |
`NVIDIA_L4` |
Nvidia L4 GPU. |
`NVIDIA_H100_80GB` |
Nvidia H100 80Gb GPU. |
`NVIDIA_H100_MEGA_80GB` |
Nvidia H100 Mega 80Gb GPU. |
`NVIDIA_H200_141GB` |
Nvidia H200 141Gb GPU. |
`NVIDIA_B200` |
Nvidia B200 GPU. |
`NVIDIA_GB200` |
Nvidia GB200 GPU. |
`NVIDIA_RTX_PRO_6000` |
Nvidia RTX Pro 6000 GPU. |
`TPU_V2` |
TPU v2. |
`TPU_V3` |
TPU v3. |
`TPU_V4_POD` |
TPU v4. |
`TPU_V5_LITEPOD` |
TPU v5. |

## Methods

### AcceleratorType

`AcceleratorType(value)`


Represents a hardware accelerator type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesAsyncPager -->

# Class ListFeaturesAsyncPager (1.134.0)

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

## Methods

### ListFeaturesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexecution__googlecloudaiplatform_v1beta1types_9a3c3b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexecution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Execution -->

# Class Execution (1.134.0)

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Execution. |
`display_name` |
`str`
User provided display name of the Execution. May be up to 128 Unicode characters. |
`state` |
The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines) and the system does not prescribe or check the validity of state transitions. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Executions. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Execution was last updated. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in `schema_title` to use.
Schema title and version is expected to be registered in
earlier Create Schema calls. And both are used together as
unique identifiers to identify schemas within the local
metadata store.
|
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Execution |

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

### State

`State(value)`


Describes the state of the Execution.

## Methods

### Execution

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general execution.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesjobstate_googlecloudaiplatform_v1beta1typescr_79f26f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesjobstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.JobState -->

# Class JobState (1.134.0)

`JobState(value)`


Describes the state of a job.

## Enums |
|
|---|---|
Name |
Description |
`JOB_STATE_UNSPECIFIED` |
The job state is unspecified. |
`JOB_STATE_QUEUED` |
The job has been just created or resumed and processing has not yet begun. |
`JOB_STATE_PENDING` |
The service is preparing to run the job. |
`JOB_STATE_RUNNING` |
The job is in progress. |
`JOB_STATE_SUCCEEDED` |
The job completed successfully. |
`JOB_STATE_FAILED` |
The job failed. |
`JOB_STATE_CANCELLING` |
The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED`, `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED`. |
`JOB_STATE_CANCELLED` |
The job has been cancelled. |
`JOB_STATE_PAUSED` |
The job has been stopped, and can be resumed. |
`JOB_STATE_EXPIRED` |
The job has expired. |
`JOB_STATE_UPDATING` |
The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state. |
`JOB_STATE_PARTIALLY_SUCCEEDED` |
The job is partially succeeded, some results may be missing due to errors. |

## Methods

### JobState

`JobState(value)`


Describes the state of a job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateArtifactRequest -->

# Class CreateArtifactRequest (1.134.0)

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Artifact should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`artifact` |
Required. The Artifact to create. |
`artifact_id` |
`str`
The {artifact} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
If not provided, the Artifact's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Artifacts in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Artifact.)
|

## Methods

### CreateArtifactRequest

`CreateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateArtifact.


---

<!-- DOCUMENTO FUSIONADO: definition_v1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/definition_v1 -->

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobspag_03d44c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobspage_72f5e7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobspager_f2ee2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobspager__c5cf08.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobspager_g_15484d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsPager -->

# Class ListBatchPredictionJobsPager (1.134.0)

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

## Methods

### ListBatchPredictionJobsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistmetadataschemaspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataSchemasPager -->

# Class ListMetadataSchemasPager (1.134.0)

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataSchemasPager

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistexecutionsasyncp_d300e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistexecutionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListExecutionsAsyncPager -->

# Class ListExecutionsAsyncPager (1.134.0)

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsAsyncPager

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListExecutionsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesexample_store_servicepagerslistexamplestorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresPager -->

# Class ListExampleStoresPager (1.134.0)

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

## Methods

### ListExampleStoresPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.featurestore_service.pagers`

module.

## Classes

[ListEntityTypesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesAsyncPager)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEntityTypesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesPager)

```
ListEntityTypesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse) object, and
provides an `__iter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesAsyncPager)

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

[ListFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesPager)

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

[ListFeaturestoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager)

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturestoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresPager)

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse) object, and
provides an `__iter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesAsyncPager)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesPager)

```
SearchFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationsp_57c9d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationspa_09a6ee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationspag_c60933.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationsPager -->

# Class ListModelEvaluationsPager (1.134.0)

```
ListModelEvaluationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
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


A pager for iterating through `list_model_evaluations`

requests.

This class thinly wraps an initial
[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_evaluations`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelEvaluations`

requests and continue to iterate
through the `model_evaluations`

field on the
corresponding responses.

All the usual [ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationsPager

```
ListModelEvaluationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplainrequestconcurrentexplanationspecoverri_290c0c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplainrequestconcurrentexplanationspecoverrideentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainRequest.ConcurrentExplanationSpecOverrideEntry -->

# Class ConcurrentExplanationSpecOverrideEntry (1.134.0)

```
ConcurrentExplanationSpecOverrideEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### ConcurrentExplanationSpecOverrideEntry

```
ConcurrentExplanationSpecOverrideEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgenerationconfigthinkingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.ThinkingConfig -->

# Class ThinkingConfig (1.134.0)

`ThinkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for thinking features.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`include_thoughts` |
`bool`
Indicates whether to include thoughts in the response. If true, thoughts are returned only when available. This field is a member of `oneof` _ `_include_thoughts` .
|
`thinking_budget` |
`int`
Optional. Indicates the thinking budget in tokens. This is only applied when enable_thinking is true. This field is a member of `oneof` _ `_thinking_budget` .
|

## Methods

### ThinkingConfig

`ThinkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for thinking features.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmigratableresource_googlecloudaiplatform_v1beta1se_102c59.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigratableresource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource -->

# Class MigratableResource (1.134.0)

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

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
`ml_engine_model_version` |
Output only. Represents one Version in ml.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_model` |
Output only. Represents one Model in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_dataset` |
Output only. Represents one Dataset in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`data_labeling_dataset` |
Output only. Represents one Dataset in datalabeling.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`last_migrate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the last migration attempt on this MigratableResource started. Will not be set if there's no migration attempt on this MigratableResource. |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MigratableResource was last updated. |

## Classes

### AutomlDataset

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

### AutomlModel

`AutomlModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Model in automl.googleapis.com.

### DataLabelingDataset

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.

### MlEngineModelVersion

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.

## Methods

### MigratableResource

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardrunspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardRunsPager -->

# Class ListTensorboardRunsPager (1.134.0)

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
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


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardRuns`

requests and continue to iterate
through the `tensorboard_runs`

field on the
corresponding responses.

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardRunsPager

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistentitytypesasync_24855f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistentitytypesasyncp_e87b9c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistentitytypesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesAsyncPager -->

# Class ListEntityTypesAsyncPager (1.134.0)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesAsyncPager

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_servicepagerslistragcorporaasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager -->

# Class ListRagCorporaAsyncPager (1.134.0)

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse) object, and
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

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagCorporaAsyncPager

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesspecialist_pool_servicepagerslistspecialistpool_5b9283.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesspecialist_pool_servicepagerslistspecialistpoolspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager -->

# Class ListSpecialistPoolsPager (1.134.0)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsPager

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturestoreonlineservingconfig_googlecloudaiplatf_47176e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoreonlineservingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Featurestore.OnlineServingConfig -->

# Class OnlineServingConfig (1.134.0)

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

## Attributes |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
The number of nodes for the online store. The number of nodes doesn't scale automatically, but you can manually update the number of nodes. If set to 0, the featurestore will not have an online store and cannot be used for online serving. |
`scaling` |
Online serving scaling configuration. Only one of `fixed_node_count` and `scaling` can be set. Setting one
will reset the other.
|

## Classes

### Scaling

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

## Methods

### OnlineServingConfig

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespythonpackagespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PythonPackageSpec -->

# Class PythonPackageSpec (1.134.0)

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.

## Attributes |
|
|---|---|
Name |
Description |
`executor_image_uri` |
`str`
Required. The URI of a container image in Artifact Registry that will run the provided Python package. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of `pre-built containers for training |
`package_uris` |
`MutableSequence[str]`
Required. The Google Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100. |
`python_module` |
`str`
Required. The Python module name to run after installing the packages. |
`args` |
`MutableSequence[str]`
Command line arguments to be passed to the Python task. |
`env` |
`MutableSequence[`
Environment variables to be passed to the python module. Maximum limit is 100. |

## Methods

### PythonPackageSpec

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationsasy_4dff30.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationsasyn_7bb406.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationsasync_66d319.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationsasyncp_9d90e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistannotationsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsAsyncPager -->

# Class ListAnnotationsAsyncPager (1.134.0)

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

## Methods

### ListAnnotationsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardsAsyncPager -->

# Class ListTensorboardsAsyncPager (1.134.0)

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
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


A pager for iterating through `list_tensorboards`

requests.

This class thinly wraps an initial
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboards`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboards`

requests and continue to iterate
through the `tensorboards`

field on the
corresponding responses.

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardsAsyncPager

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistsavedqueriesasync_fa22b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistsavedqueriesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesAsyncPager -->

# Class ListSavedQueriesAsyncPager (1.134.0)

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

## Methods

### ListSavedQueriesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmemory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory -->

# Class Memory (1.134.0)

`Memory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory.

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
Optional. Timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what `expiration` was sent on input.
This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. Input only. The TTL for this resource. The expiration time is computed: now + TTL. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Identifier. The resource name of the Memory. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/memories/{memory}`
|
`display_name` |
`str`
Optional. Display name of the Memory. |
`description` |
`str`
Optional. Description of the Memory. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Memory was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Memory was most recently updated. |
`fact` |
`str`
Required. Semantic knowledge extracted from the source content. |
`scope` |
`MutableMapping[str, str]`
Required. Immutable. The scope of the Memory. Memories are isolated within their scope. The scope is defined when creating or generating memories. Scope values cannot contain the wildcard character '\*'. |

## Classes

### ScopeEntry

`ScopeEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### Memory

`Memory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvizier_servicepagers__googlecloudaiplatfor_b4b763.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.vizier_service.pagers`

module.

## Classes

[ListStudiesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesAsyncPager)

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse) object, and
provides an `__aiter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListStudiesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesPager)

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

[ListTrialsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsAsyncPager)

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListTrialsResponse,
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
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse) object, and
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

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrialsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListTrialsPager)

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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookruntimes_093a7a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookruntimespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesPager -->

# Class ListNotebookRuntimesPager (1.134.0)

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesPager

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelversionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionsAsyncPager -->

# Class ListModelVersionsAsyncPager (1.134.0)

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
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


A pager for iterating through `list_model_versions`

requests.

This class thinly wraps an initial
[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersions`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionsAsyncPager

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesclassificati_368944.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesclassificatio_479cc1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesclassification_51123e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesclassificationp_eb31c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesclassificationpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ClassificationPredictionResult -->

# Class ClassificationPredictionResult (1.134.0)

```
ClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image and Text Classification.

## Attributes |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[int]`
The resource IDs of the AnnotationSpecs that had been identified. |
`display_names` |
`MutableSequence[str]`
The display names of the AnnotationSpecs that had been identified, order matches the IDs. |
`confidences` |
`MutableSequence[float]`
The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids. |

## Methods

### ClassificationPredictionResult

```
ClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image and Text Classification.

### ClassificationPredictionResult

```
ClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image and Text Classification.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideoclassificationinputsmodeltype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassificationInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which cannot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_JETSON_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) to a Jetson device afterwards.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespythonpackagespec_googlecloudaiplatform_v1typ_e3c78e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespythonpackagespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PythonPackageSpec -->

# Class PythonPackageSpec (1.134.0)

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.

## Attributes |
|
|---|---|
Name |
Description |
`executor_image_uri` |
`str`
Required. The URI of a container image in Artifact Registry that will run the provided Python package. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of `pre-built containers for training |
`package_uris` |
`MutableSequence[str]`
Required. The Google Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100. |
`python_module` |
`str`
Required. The Python module name to run after installing the packages. |
`args` |
`MutableSequence[str]`
Command line arguments to be passed to the Python task. |
`env` |
`MutableSequence[`
Environment variables to be passed to the python module. Maximum limit is 100. |

## Methods

### PythonPackageSpec

`PythonPackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Python packaged code.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdnspeeringconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DnsPeeringConfig -->

# Class DnsPeeringConfig (1.134.0)

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

## Attributes |
|
|---|---|
Name |
Description |
`domain` |
`str`
Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot. |
`target_project` |
`str`
Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Vertex AI Service Agent requires the dns.peer role on this project. |
`target_network` |
`str`
Required. The VPC network name in the target_project where the DNS zone specified by 'domain' is visible. |

## Methods

### DnsPeeringConfig

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfea_8a3ec3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfeatureviewspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager -->

# Class ListFeatureViewsPager (1.134.0)

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewsPager

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigratableresource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource -->

# Class MigratableResource (1.134.0)

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

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
`ml_engine_model_version` |
Output only. Represents one Version in ml.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_model` |
Output only. Represents one Model in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`automl_dataset` |
Output only. Represents one Dataset in automl.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`data_labeling_dataset` |
Output only. Represents one Dataset in datalabeling.googleapis.com. This field is a member of `oneof` _ `resource` .
|
`last_migrate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the last migration attempt on this MigratableResource started. Will not be set if there's no migration attempt on this MigratableResource. |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MigratableResource was last updated. |

## Classes

### AutomlDataset

`AutomlDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in automl.googleapis.com.

### AutomlModel

`AutomlModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Model in automl.googleapis.com.

### DataLabelingDataset

`DataLabelingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Dataset in datalabeling.googleapis.com.

### MlEngineModelVersion

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.

## Methods

### MigratableResource

`MigratableResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one resource that exists in automl.googleapis.com, datalabeling.googleapis.com or ml.googleapis.com.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesdataset_servicepagerssearchdataitemsasync_042352.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerssearchdataitemsasyncp_9b8363.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerssearchdataitemsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsAsyncPager -->

# Class SearchDataItemsAsyncPager (1.134.0)

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

## Methods

### SearchDataItemsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistnastrialdetailsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsAsyncPager -->

# Class ListNasTrialDetailsAsyncPager (1.134.0)

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

## Methods

### ListNasTrialDetailsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesexample_store_servicepagersfetchexamplesas_7760e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesexample_store_servicepagersfetchexamplesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesAsyncPager -->

# Class FetchExamplesAsyncPager (1.134.0)

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

## Methods

### FetchExamplesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragfilesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager -->

# Class ListRagFilesAsyncPager (1.134.0)

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

## Methods

### ListRagFilesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfea_50a184.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeat_3af70a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeatu_e69309.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeatur_ba5190.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeature_a47a67.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeatureg_e7398b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturegroupspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsPager -->

# Class ListFeatureGroupsPager (1.134.0)

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

## Methods

### ListFeatureGroupsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmonitorspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitorsPager -->

# Class ListModelMonitorsPager (1.134.0)

```
ListModelMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
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


A pager for iterating through `list_model_monitors`

requests.

This class thinly wraps an initial
[ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_monitors`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelMonitors`

requests and continue to iterate
through the `model_monitors`

field on the
corresponding responses.

All the usual [ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitorsPager

```
ListModelMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicespipeline_servicepagerslisttrainingpipeline_873aa2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_servicepagerslisttrainingpipelinespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesPager -->

# Class ListTrainingPipelinesPager (1.134.0)

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

## Methods

### ListTrainingPipelinesPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigrateresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest -->

# Class MigrateResourceRequest (1.134.0)

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`migrate_ml_engine_model_version_config` |
Config for migrating Version in ml.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_model_config` |
Config for migrating Model in automl.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_dataset_config` |
Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|
`migrate_data_labeling_dataset_config` |
Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|

## Classes

### MigrateAutomlDatasetConfig

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.

### MigrateAutomlModelConfig

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.

### MigrateDataLabelingDatasetConfig

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.

### MigrateMlEngineModelVersionConfig

```
MigrateMlEngineModelVersionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating version in ml.googleapis.com to Vertex AI's Model.

## Methods

### MigrateResourceRequest

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerssearchfeaturesa_0c45c0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerssearchfeaturesas_0e3151.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerssearchfeaturesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesAsyncPager -->

# Class SearchFeaturesAsyncPager (1.134.0)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchFeaturesAsyncPager

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagerslistindexendpointspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsPager -->

# Class ListIndexEndpointsPager (1.134.0)

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexEndpointsPager

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistbatchpredictionjobspa_2f4a98.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistbatchpredictionjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsPager -->

# Class ListBatchPredictionJobsPager (1.134.0)

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

## Methods

### ListBatchPredictionJobsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigrateresourcerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest -->

# Class MigrateResourceRequest (1.134.0)

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`migrate_ml_engine_model_version_config` |
Config for migrating Version in ml.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_model_config` |
Config for migrating Model in automl.googleapis.com to Vertex AI's Model. This field is a member of `oneof` _ `request` .
|
`migrate_automl_dataset_config` |
Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|
`migrate_data_labeling_dataset_config` |
Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset. This field is a member of `oneof` _ `request` .
|

## Classes

### MigrateAutomlDatasetConfig

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.

### MigrateAutomlModelConfig

`MigrateAutomlModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Model in automl.googleapis.com to Vertex AI's Model.

### MigrateDataLabelingDatasetConfig

```
MigrateDataLabelingDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating Dataset in datalabeling.googleapis.com to Vertex AI's Dataset.

### MigrateMlEngineModelVersionConfig

```
MigrateMlEngineModelVersionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating version in ml.googleapis.com to Vertex AI's Model.

## Methods

### MigrateResourceRequest

`MigrateResourceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config of migrating one resource from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesreasoning_engine_servicepagerslistreasoningen_7f2e01.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesreasoning_engine_servicepagerslistreasoningeng_9ef5bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesreasoning_engine_servicepagerslistreasoningengi_eb5ffa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesreasoning_engine_servicepagerslistreasoningenginespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesPager -->

# Class ListReasoningEnginesPager (1.134.0)

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse) object, and
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

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListReasoningEnginesPager

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadatastoresasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresAsyncPager -->

# Class ListMetadataStoresAsyncPager (1.134.0)

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
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


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataStoresAsyncPager

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_garden_servicepagerslistpublishermod_025d10.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_garden_servicepagerslistpublishermodelspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsPager -->

# Class ListPublisherModelsPager (1.134.0)

```
ListPublisherModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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


A pager for iterating through `list_publisher_models`

requests.

This class thinly wraps an initial
[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`publisher_models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPublisherModels`

requests and continue to iterate
through the `publisher_models`

field on the
corresponding responses.

All the usual [ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPublisherModelsPager

```
ListPublisherModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_tuning_servicepagerslisttuningjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsAsyncPager -->

# Class ListTuningJobsAsyncPager (1.134.0)

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

## Methods

### ListTuningJobsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturestoresasy_6b6ff9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturestoresasyn_57c33d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturestoresasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager -->

# Class ListFeaturestoresAsyncPager (1.134.0)

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturestoresAsyncPager

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsAsyncPager -->

# Class ListDataLabelingJobsAsyncPager (1.134.0)

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

## Methods

### ListDataLabelingJobsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typessummarizationverbosityresult_googlecloudaiplatfor_f5c979.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessummarizationverbosityresult_googlecloudaiplatform_428f47.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessummarizationverbosityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationVerbosityResult -->

# Class SummarizationVerbosityResult (1.134.0)

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Verbosity score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization verbosity score. |
`confidence` |
`float`
Output only. Confidence for summarization verbosity score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationVerbosityResult

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprivateendpoints.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PrivateEndpoints -->

# Class PrivateEndpoints (1.134.0)

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

## Attributes |
|
|---|---|
Name |
Description |
`predict_http_uri` |
`str`
Output only. Http(s) path to send prediction requests. |
`explain_http_uri` |
`str`
Output only. Http(s) path to send explain requests. |
`health_http_uri` |
`str`
Output only. Http(s) path to send health check requests. |
`service_attachment` |
`str`
Output only. The name of the service attachment resource. Populated if private service connect is enabled. |

## Methods

### PrivateEndpoints

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_servicepagerslistpipelinejobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager -->

# Class ListPipelineJobsAsyncPager (1.134.0)

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

## Methods

### ListPipelineJobsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagers____googlecloudaiplatform_v1se_a1729b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers -->

# Module pagers (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadataschemasasyn_f6137c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadataschemasasync_cbf8a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadataschemasasyncp_deea2b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadataschemasasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasAsyncPager -->

# Class ListMetadataSchemasAsyncPager (1.134.0)

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataSchemasAsyncPager

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationslicespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationSlicesPager -->

# Class ListModelEvaluationSlicesPager (1.134.0)

```
ListModelEvaluationSlicesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
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


A pager for iterating through `list_model_evaluation_slices`

requests.

This class thinly wraps an initial
[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse) object, and
provides an `__iter__`

method to iterate through its
`model_evaluation_slices`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelEvaluationSlices`

requests and continue to iterate
through the `model_evaluation_slices`

field on the
corresponding responses.

All the usual [ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationSlicesPager

```
ListModelEvaluationSlicesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistentitytypesa_4b3689.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistentitytypesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesAsyncPager -->

# Class ListEntityTypesAsyncPager (1.134.0)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesAsyncPager

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrawpredictrequest_googlecloudaiplatform_v1typesdyn_9c35f5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RawPredictRequest -->

# Class RawPredictRequest (1.134.0)

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.

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
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the `Model` as a `DeployedModel`
to an Endpoint and
use the `RawPredict` method.
|

## Methods

### RawPredictRequest

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdynamicretrievalconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DynamicRetrievalConfig -->

# Class DynamicRetrievalConfig (1.134.0)

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`mode` |
The mode of the predictor to be used in dynamic retrieval. |
`dynamic_threshold` |
`float`
Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used. This field is a member of `oneof` _ `_dynamic_threshold` .
|

## Classes

### Mode

`Mode(value)`


The mode of the predictor to be used in dynamic retrieval.

## Methods

### DynamicRetrievalConfig

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformvideodataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.VideoDataset -->

# Class VideoDataset (1.134.0)

```
VideoDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


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

### VideoDataset

```
VideoDataset(
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
) -> google.cloud.aiplatform.datasets.video_dataset.VideoDataset
```


Creates a new video dataset.

Optionally imports data into the dataset when a source and
`import_schema_uri`

are passed in. The following is an example of how
this method is used:

```
my_dataset = aiplatform.VideoDataset.create(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=['gs://aip.schema.dataset.ioformat.video.classification.yaml']
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
The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`import_schema_uri` |
`str`
A URI for a YAML file stored in Cloud Storage that describes the import schema used to validate the dataset. The schema is an |
`data_item_labels` |
`Dict`
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each item in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Dataset items are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
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
`video_dataset (VideoDataset)` |
An instantiated representation of the managed `VideoDataset` resource. |

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspeci_0c2735.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspecia_09a479.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspecial_c768a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspeciali_0dc08f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspecialis_6cefe4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspecialistpoolspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager -->

# Class ListSpecialistPoolsPager (1.134.0)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsPager

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragcorporaasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager -->

# Class ListRagCorporaAsyncPager (1.134.0)

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

## Methods

### ListRagCorporaAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployedmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel -->

# Class DeployedModel (1.134.0)

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

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
`dedicated_resources` |
A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`automatic_resources` |
A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`shared_resources` |
`str`
The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
This field is a member of `oneof` _ `prediction_resources` .
|
`full_fine_tuned_resources` |
Optional. Resources for a full fine tuned model. This field is a member of `oneof` _ `prediction_resources` .
|
`id` |
`str`
Immutable. The ID of the DeployedModel. If not provided upon deployment, Vertex AI will generate a value for this ID. This value should be 1-10 characters, and valid characters are `/[0-9]/` .
|
`model` |
`str`
The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint. The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
if no version is specified, the default version will be
deployed.
|
`model_version_id` |
`str`
Output only. The version ID of the model that is deployed. |
`display_name` |
`str`
The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedModel was created. |
`explanation_spec` |
Explanation configuration for this DeployedModel. When deploying a Model using EndpointService.DeployModel, this value overrides the value of Model.explanation_spec. All fields of explanation_spec are optional in the request. If a field of explanation_spec is not populated, the value of the same field of Model.explanation_spec is inherited. If the corresponding Model.explanation_spec is not populated, all fields of the explanation_spec will be used for the explanation configuration. |
`disable_explanations` |
`bool`
If true, deploy the model without explainable feature, regardless the existence of Model.explanation_spec or explanation_spec. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`enable_container_logging` |
`bool`
If true, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging.
Only supported for custom-trained Models and AutoML Tabular
Models.
|
`disable_container_logging` |
`bool`
For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`enable_access_logging` |
`bool`
If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request. Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`private_endpoints` |
Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if network is configured. |
`faster_deployment_config` |
Configuration for faster model deployment. |
`rollout_options` |
Options for configuring rolling deployments. |
`status` |
Output only. Runtime status of the deployed model. |
`system_labels` |
`MutableMapping[str, str]`
System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`checkpoint_id` |
`str`
The checkpoint id of the model. |
`speculative_decoding_spec` |
Optional. Spec for configuring speculative decoding. |

## Classes

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DeployedModel

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadata_googleclo_6581c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadata_googleclou_43adbd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadata_googlecloud_ebac82.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata -->

# Class NearestNeighborSearchOperationMetadata (1.134.0)

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.

## Attributes |
|
|---|---|
Name |
Description |
`content_validation_stats` |
`MutableSequence[`
The validation stats of the content (per file) to be inserted or updated on the Matching Engine Index resource. Populated if contentsDeltaUri is provided as part of Index.metadata. Please note that, currently for those files that are broken or has unsupported file format, we will not have the stats for those files. |
`data_bytes_count` |
`int`
The ingested data size in bytes. |

## Classes

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### NearestNeighborSearchOperationMetadata

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrecommendspecrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecRequest -->

# Class RecommendSpecRequest (1.134.0)

`RecommendSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.RecommendSpec.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to recommend specs. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`gcs_uri` |
`str`
Required. The Google Cloud Storage URI of the custom model, storing weights and config files (which can be used to infer the base model). |
`check_machine_availability` |
`bool`
Optional. If true, check machine availability for the recommended regions. Only return the machine spec in regions where the machine is available. |
`check_user_quota` |
`bool`
Optional. If true, check user quota for the recommended regions. Returns all the machine spec in regions they are available, and also the user quota state for each machine type in each region. |

## Methods

### RecommendSpecRequest

`RecommendSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.RecommendSpec.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetversionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager -->

# Class ListDatasetVersionsAsyncPager (1.134.0)

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

## Methods

### ListDatasetVersionsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespublishermodelcalltoactiondeploydeploymetadata_go_3cf5b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelcalltoactiondeploydeploymetadata_goo_c865c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelcalltoactiondeploydeploymetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.Deploy.DeployMetadata -->

# Class DeployMetadata (1.134.0)

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Attributes |
|
|---|---|
Name |
Description |
`labels` |
`MutableMapping[str, str]`
Optional. Labels for the deployment. For managing deployment config like verifying, source of deployment config, etc. |
`sample_request` |
`str`
Optional. Sample request for deployed endpoint. |

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

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoreonlineservingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore.OnlineServingConfig -->

# Class OnlineServingConfig (1.134.0)

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

## Attributes |
|
|---|---|
Name |
Description |
`fixed_node_count` |
`int`
The number of nodes for the online store. The number of nodes doesn't scale automatically, but you can manually update the number of nodes. If set to 0, the featurestore will not have an online store and cannot be used for online serving. |
`scaling` |
Online serving scaling configuration. Only one of `fixed_node_count` and `scaling` can be set. Setting one
will reset the other.
|

## Classes

### Scaling

`Scaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Online serving scaling configuration. If min_node_count and max_node_count are set to the same value, the cluster will be configured with the fixed number of node (no auto-scaling).

## Methods

### OnlineServingConfig

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationsAsyncPager -->

# Class ListModelEvaluationsAsyncPager (1.134.0)

```
ListModelEvaluationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
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


A pager for iterating through `list_model_evaluations`

requests.

This class thinly wraps an initial
[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_evaluations`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelEvaluations`

requests and continue to iterate
through the `model_evaluations`

field on the
corresponding responses.

All the usual [ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationsAsyncPager

```
ListModelEvaluationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicessession_servicepagers___googlecloudaiplat_3455a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicessession_servicepagers___googlecloudaiplatf_b7ff45.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.session_service.pagers`

module.

## Classes

[ListEventsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsAsyncPager)

```
ListEventsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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


A pager for iterating through `list_events`

requests.

This class thinly wraps an initial
[ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse) object, and
provides an `__aiter__`

method to iterate through its
`session_events`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEvents`

requests and continue to iterate
through the `session_events`

field on the
corresponding responses.

All the usual [ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEventsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsPager)

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

[ListSessionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsAsyncPager)

```
ListSessionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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


A pager for iterating through `list_sessions`

requests.

This class thinly wraps an initial
[ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`sessions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSessions`

requests and continue to iterate
through the `sessions`

field on the
corresponding responses.

All the usual [ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSessionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsPager)

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


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlfore_b4d8e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforec_0877f1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastinginputstransformationtexttransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.TextTransformation -->

# Class TextTransformation (1.134.0)

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The text as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


## Methods

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The text as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The text as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmetadataschemasrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasRequest -->

# Class ListMetadataSchemasRequest (1.134.0)

`ListMetadataSchemasRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataSchemas.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose MetadataSchemas should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of MetadataSchemas to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListMetadataSchemas call. Provide this to retrieve the next page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |
`filter` |
`str`
A query to filter available MetadataSchemas for matching results. |

## Methods

### ListMetadataSchemasRequest

`ListMetadataSchemasRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListMetadataSchemas.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreateexecutionrequest_googlecloudaiplatform_v1bet_4b4dd9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateExecutionRequest -->

# Class CreateExecutionRequest (1.134.0)

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Execution should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`execution` |
Required. The Execution to create. |
`execution_id` |
`str`
The {execution} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
If not provided, the Execution's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Executions in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Execution.)
|

## Methods

### CreateExecutionRequest

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessummarizationverbosityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityResult -->

# Class SummarizationVerbosityResult (1.134.0)

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Verbosity score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization verbosity score. |
`confidence` |
`float`
Output only. Confidence for summarization verbosity score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationVerbosityResult

```
SummarizationVerbosityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization verbosity result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesgen_ai_cache_servicepagerslistcachedcontentsas_ab57a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesgen_ai_cache_servicepagerslistcachedcontentsasy_d76505.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_cache_servicepagerslistcachedcontentsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager -->

# Class ListCachedContentsAsyncPager (1.134.0)

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse,
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


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCachedContentsAsyncPager

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelversioncheckpointspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionCheckpointsPager -->

# Class ListModelVersionCheckpointsPager (1.134.0)

```
ListModelVersionCheckpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
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


A pager for iterating through `list_model_version_checkpoints`

requests.

This class thinly wraps an initial
[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`checkpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelVersionCheckpoints`

requests and continue to iterate
through the `checkpoints`

field on the
corresponding responses.

All the usual [ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionCheckpointsPager

```
ListModelVersionCheckpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturem_649edd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturemonitorspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsPager -->

# Class ListFeatureMonitorsPager (1.134.0)

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

## Methods

### ListFeatureMonitorsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardsAsyncPager -->

# Class ListTensorboardsAsyncPager (1.134.0)

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
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


A pager for iterating through `list_tensorboards`

requests.

This class thinly wraps an initial
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboards`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboards`

requests and continue to iterate
through the `tensorboards`

field on the
corresponding responses.

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardsAsyncPager

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmatch_servicematchserviceclient_____googlecloud_be79f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmatch_servicematchserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient -->

# Class MatchServiceClient (1.134.0)

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescreatemetadatastorerequest_googlecloudaiplatfor_6625cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescreatemetadatastorerequest_googlecloudaiplatform_f981d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreatemetadatastorerequest_googlecloudaiplatform__b7fb6a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatemetadatastorerequest_googlecloudaiplatform_v_cc038b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatemetadatastorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataStoreRequest -->

# Class CreateMetadataStoreRequest (1.134.0)

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location where the MetadataStore should be created. Format: `projects/{project}/locations/{location}/`
|
`metadata_store` |
Required. The MetadataStore to create. |
`metadata_store_id` |
`str`
The {metadatastore} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataStores in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataStore.)
|

## Methods

### CreateMetadataStoreRequest

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatetensorboardexperimentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardExperimentRequest -->

# Class UpdateTensorboardExperimentRequest (1.134.0)

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardExperiment resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_experiment` |
Required. The TensorboardExperiment's `name` field is used
to identify the TensorboardExperiment to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### UpdateTensorboardExperimentRequest

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnastrialdetailsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsAsyncPager -->

# Class ListNasTrialDetailsAsyncPager (1.134.0)

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

## Methods

### ListNasTrialDetailsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelsourceinfomodelsourcetype_googlecloudaiplatf_e11167.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelsourceinfomodelsourcetype_googlecloudaiplatfo_166a67.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelsourceinfomodelsourcetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelSourceInfo.ModelSourceType -->

# Class ModelSourceType (1.134.0)

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Enums |
|
|---|---|
Name |
Description |
`MODEL_SOURCE_TYPE_UNSPECIFIED` |
Should not be used. |
`AUTOML` |
The Model is uploaded by automl training pipeline. |
`CUSTOM` |
The Model is uploaded by user or custom training pipeline. |
`BQML` |
The Model is registered and sync'ed from BigQuery ML. |
`MODEL_GARDEN` |
The Model is saved or tuned from Model Garden. |
`GENIE` |
The Model is saved or tuned from Genie. |
`CUSTOM_TEXT_EMBEDDING` |
The Model is uploaded by text embedding finetuning pipeline. |
`MARKETPLACE` |
The Model is saved or tuned from Marketplace. |

## Methods

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturevaluesresponseselecttimerangeandfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesResponse.SelectTimeRangeAndFeature -->

# Class SelectTimeRangeAndFeature (1.134.0)

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.

## Attributes |
|
|---|---|
Name |
Description |
`impacted_feature_count` |
`int`
The count of the features or columns impacted. This is the same as the feature count in the request. |
`offline_storage_modified_entity_row_count` |
`int`
The count of modified entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. Within each row, only the features specified in the request are deleted. |
`online_storage_modified_entity_count` |
`int`
The count of modified entities in the online storage. Each entity ID corresponds to one entity. Within each entity, only the features specified in the request are deleted. |

## Methods

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatemetadatastorerequest_googlecloudaiplatf_484082.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatemetadatastorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataStoreRequest -->

# Class CreateMetadataStoreRequest (1.134.0)

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location where the MetadataStore should be created. Format: `projects/{project}/locations/{location}/`
|
`metadata_store` |
Required. The MetadataStore to create. |
`metadata_store_id` |
`str`
The {metadatastore} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataStores in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataStore.)
|

## Methods

### CreateMetadataStoreRequest

`CreateMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExecutionRequest -->

# Class CreateExecutionRequest (1.134.0)

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Execution should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`execution` |
Required. The Execution to create. |
`execution_id` |
`str`
The {execution} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
If not provided, the Execution's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Executions in the parent MetadataStore. (Otherwise the
request will fail with ALREADY_EXISTS, or PERMISSION_DENIED
if the caller can't view the preexisting Execution.)
|

## Methods

### CreateExecutionRequest

`CreateExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateExecution.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegroup_8ce32a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegroups_791898.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegroupsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager -->

# Class ListFeatureGroupsAsyncPager (1.134.0)

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
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
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse) object, and
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

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureGroupsAsyncPager

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager -->

# Class ListNotebookRuntimesAsyncPager (1.134.0)

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesAsyncPager

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersquerydepl_3fbbda.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersquerydeployedmodelspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager -->

# Class QueryDeployedModelsPager (1.134.0)

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__iter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsPager

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdynamicretrievalconfig_googlecloudaiplatform__41484b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdynamicretrievalconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DynamicRetrievalConfig -->

# Class DynamicRetrievalConfig (1.134.0)

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`mode` |
The mode of the predictor to be used in dynamic retrieval. |
`dynamic_threshold` |
`float`
Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used. This field is a member of `oneof` _ `_dynamic_threshold` .
|

## Classes

### Mode

`Mode(value)`


The mode of the predictor to be used in dynamic retrieval.

## Methods

### DynamicRetrievalConfig

`DynamicRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the options to customize dynamic retrieval.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesserviceaccountspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ServiceAccountSpec -->

# Class ServiceAccountSpec (1.134.0)

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
