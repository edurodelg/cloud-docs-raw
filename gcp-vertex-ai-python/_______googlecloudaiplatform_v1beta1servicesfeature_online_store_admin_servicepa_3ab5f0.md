---
merged_at: 2026-01-27T07:03:44.004813
merged_files: 2
---


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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager -->

# Class ListFeatureViewsAsyncPager (1.134.0)

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewsAsyncPager

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.StringFilter -->

# Class StringFilter (1.134.0)

`StringFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


String filter is used to search a subset of the entities by using boolean rules on string columns. For example: if a query specifies string filter with 'name = color, allow_tokens = {red, blue}, deny_tokens = {purple}',' then that query will match entities that are red or blue, but if those points are also purple, then they will be excluded even if they are red/blue. Only string filter is supported for now, numeric filter will be supported in the near future.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Column names in BigQuery that used as filters. |
`allow_tokens` |
`MutableSequence[str]`
Optional. The allowed tokens. |
`deny_tokens` |
`MutableSequence[str]`
Optional. The denied tokens. |

## Methods

### StringFilter

`StringFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


String filter is used to search a subset of the entities by using boolean rules on string columns. For example: if a query specifies string filter with 'name = color, allow_tokens = {red, blue}, deny_tokens = {purple}',' then that query will match entities that are red or blue, but if those points are also purple, then they will be excluded even if they are red/blue. Only string filter is supported for now, numeric filter will be supported in the near future.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesRequest -->

# Class SearchMigratableResourcesRequest (1.134.0)

```
SearchMigratableResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.SearchMigratableResources.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The standard page size. The default and maximum value is 100. |
`page_token` |
`str`
The standard page token. |
`filter` |
`str`
A filter for your search. You can use the following types of filters: - Resource type filters. The following strings filter for a specific type of MigratableResource: - `ml_engine_model_version:*`
- `automl_model:*`
- `automl_dataset:*`
- `data_labeling_dataset:*`
- "Migrated or not" filters. The following strings filter
for resources that either have or have not already been
migrated:
- `last_migrate_time:*` filters for migrated resources.
- `NOT last_migrate_time:*` filters for not yet migrated
resources.
|

## Methods

### SearchMigratableResourcesRequest

```
SearchMigratableResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.SearchMigratableResources.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec.MultiTrialAlgorithmSpec -->

# Class MultiTrialAlgorithmSpec (1.134.0)

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm` |
The multi-trial Neural Architecture Search (NAS) algorithm type. Defaults to `REINFORCEMENT_LEARNING` .
|
`metric` |
Metric specs for the NAS job. Validation for this field is done at `multi_trial_algorithm_spec` field.
|
`search_trial_spec` |
Required. Spec for search trials. |
`train_trial_spec` |
Spec for train trials. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Classes

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

### MultiTrialAlgorithm

`MultiTrialAlgorithm(value)`


The available types of multi-trial algorithms.

### SearchTrialSpec

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Methods

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetBatchPredictionJobRequest -->

# Class GetBatchPredictionJobRequest (1.134.0)

```
GetBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob resource. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### GetBatchPredictionJobRequest

```
GetBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetBatchPredictionJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringQualitySpec -->

# Class QuestionAnsweringQualitySpec (1.134.0)

```
QuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality score metric.

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

### QuestionAnsweringQualitySpec

```
QuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager -->

# Class SearchMigratableResourcesAsyncPager (1.134.0)

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchMigratableResourcesAsyncPager

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager -->

# Class ListNotebookExecutionJobsAsyncPager (1.134.0)

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookExecutionJobsAsyncPager

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsRequest -->

# Class ListPipelineJobsRequest (1.134.0)

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the PipelineJobs that match the filter expression. The following fields are supported: - `pipeline_name` : Supports `=` and `!=` comparisons.
- `display_name` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `pipeline_job_user_id` : Supports `=` , `!=`
comparisons, and `:` wildcard. for example, can check if
pipeline's display_name contains *step* by doing
display_name:"*step*"
- `state` : Supports `=` and `!=` comparisons.
- `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `end_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
- `template_uri` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `template_metadata.version` : Supports `=` , `!=`
comparisons, and `:` wildcard.
Filter expressions can be combined together using logical
operators (`AND` & `OR` ). For example:
`pipeline_name="test" AND create_time>"2020-05-18T13:30:00Z"` .
The syntax to define filter expression is based on
https://google.aip.dev/160.
Examples:
- `create_time>"2021-05-18T00:00:00Z" OR update_time>"2020-05-18T00:00:00Z"`
PipelineJobs created or updated after 2020-05-18 00:00:00
UTC.
- `labels.env = "prod"` PipelineJobs with label "env" set
to "prod".
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListPipelineJobsResponse.next_page_token of the previous PipelineService.ListPipelineJobs call. |
`order_by` |
`str`
A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple order_by fields provided e.g. "create_time desc, end_time", "end_time, start_time, update_time" For example, using "create_time desc, end_time" will order results by create time in descending order, and if there are multiple jobs having the same create time, order them by the end time in ascending order. if order_by is not specified, it will order by default order is create time in descending order. Supported fields: - `create_time`
- `update_time`
- `end_time`
- `start_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListPipelineJobsRequest

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile -->

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
`size_bytes` |
`int`
Output only. The size of the RagFile in bytes. |
`rag_file_type` |
Output only. The type of the RagFile. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was last updated. |
`file_status` |
Output only. State of the RagFile. |
`user_metadata` |
`str`
Output only. The metadata for metadata search. The user_metadata Needs to be in JSON format. |

## Classes

### RagFileType

`RagFileType(value)`


The type of the RagFile.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager -->

# Class ListReasoningEnginesAsyncPager (1.134.0)

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

## Methods

### ListReasoningEnginesAsyncPager

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest -->

# Class AugmentPromptRequest (1.134.0)

`AugmentPromptRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for AugmentPrompt.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This field is a member of `oneof` _ `data_source` .
|
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`contents` |
`MutableSequence[`
Optional. Input content to augment, only text format is supported for now. |
`model` |
Optional. Metadata of the backend deployed model. |

## Classes

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the backend deployed model.

## Methods

### AugmentPromptRequest

`AugmentPromptRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for AugmentPrompt.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion -->

# Class DatasetVersion (1.134.0)

`DatasetVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the dataset version.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Identifier. The resource name of the DatasetVersion. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DatasetVersion was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DatasetVersion was last updated. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`big_query_dataset_name` |
`str`
Output only. Name of the associated BigQuery dataset. |
`display_name` |
`str`
The user-defined name of the DatasetVersion. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Required. Output only. Additional information about the DatasetVersion. |
`model_reference` |
`str`
Output only. Reference to the public base model last used by the dataset version. Only set for prompt dataset versions. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Methods

### DatasetVersion

`DatasetVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the dataset version.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesRequest -->

# Class ListFeaturesRequest (1.134.0)

`ListFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list Features. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`filter` |
`str`
Lists the Features that match the filter expression. The following filters are supported: - `value_type` : Supports = and != comparisons.
- `create_time` : Supports =, !=, <,>, >=, and <= comparisons.="" values="" must="" be="" in="" rfc="" 3339="" format.="" -="">`update_time` : Supports =, !=, <,>, >=, and <= comparisons.="" values="" must="" be="" in="" rfc="" 3339="" format.="" -="">`labels` : Supports key-value equality as well as key
presence.
Examples:
- `value_type = DOUBLE` --> Features whose type is DOUBLE.
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` --> Features
having both (active: yes) and (env: prod) labels.
- `labels.env: *` --> Any Feature which has a label with
'env' as the key.
|
`page_size` |
`int`
The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 1000 Features will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListFeatures call or FeatureRegistryService.ListFeatures call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListFeatures or FeatureRegistryService.ListFeatures must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `feature_id`
- `value_type` (Not supported for FeatureRegistry Feature)
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`latest_stats_count` |
`int`
Only applicable for Vertex AI Feature Store (Legacy). If set, return the most recent ListFeaturesRequest.latest_stats_count of stats for each Feature in response. Valid value is [0, 10]. If number of stats exists <>ListFeaturesRequest.latest_stats_count, return all existing stats. |

## Methods

### ListFeaturesRequest

`ListFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotation -->

# Class EvaluatedAnnotation (1.134.0)

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Output only. Type of the EvaluatedAnnotation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The model predicted annotations. For true positive, there is one and only one prediction, which matches the only one ground truth annotation in ground_truths. For false positive, there is one and only one prediction, which doesn't match any ground truth annotation of the corresponding `data_item_view_id][EvaluatedAnnotation.data_item_view_id]` .
For false negative, there are zero or more predictions which
are similar to the only ground truth annotation in
ground_truths
but not enough for a match.
The schema of the prediction is stored in
[ModelEvaluation.annotation_schema_uri][]
|
`ground_truths` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The ground truth Annotations, i.e. the Annotations that exist in the test data the Model is evaluated on. For true positive, there is one and only one ground truth annotation, which matches the only prediction in predictions. For false positive, there are zero or more ground truth annotations that are similar to the only prediction in predictions, but not enough for a match. For false negative, there is one and only one ground truth annotation, which doesn't match any predictions created by the model. The schema of the ground truth is stored in [ModelEvaluation.annotation_schema_uri][] |
`data_item_payload` |
`google.protobuf.struct_pb2.Value`
Output only. The data item payload that the Model predicted this EvaluatedAnnotation on. |
`evaluated_data_item_view_id` |
`str`
Output only. ID of the EvaluatedDataItemView under the same ancestor ModelEvaluation. The EvaluatedDataItemView consists of all ground truths and predictions on data_item_payload. |
`explanations` |
`MutableSequence[`
Explanations of predictions. Each element of the explanations indicates the explanation for one explanation Method. The attributions list in the EvaluatedAnnotationExplanation.explanation object corresponds to the predictions list. For example, the second element in the attributions list explains the second element in the predictions list. |
`error_analysis_annotations` |
`MutableSequence[`
Annotations of model error analysis results. |

## Classes

### EvaluatedAnnotationType

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined

## Methods

### EvaluatedAnnotation

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation -->

# Class NumericArrayTransformation (1.134.0)

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardRequest -->

# Class CreateTensorboardRequest (1.134.0)

`CreateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.CreateTensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Tensorboard in. Format: `projects/{project}/locations/{location}`
|
`tensorboard` |
Required. The Tensorboard to create. |

## Methods

### CreateTensorboardRequest

`CreateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.CreateTensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventRequest -->

# Class AppendEventRequest (1.134.0)

`AppendEventRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.AppendEvent.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the session to append event to. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|
`event` |
Required. The event to append to the session. |

## Methods

### AppendEventRequest

`AppendEventRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.AppendEvent.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TokensInfo -->

# Class TokensInfo (1.134.0)

`TokensInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tokens info with a list of tokens and the corresponding list of token ids.

## Attributes |
|
|---|---|
Name |
Description |
`tokens` |
`MutableSequence[bytes]`
A list of tokens from the input. |
`token_ids` |
`MutableSequence[int]`
A list of token ids from the input. |
`role` |
`str`
Optional. Optional fields for the role from the corresponding Content. |

## Methods

### TokensInfo

`TokensInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tokens info with a list of tokens and the corresponding list of token ids.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataSchema.MetadataSchemaType -->

# Class MetadataSchemaType (1.134.0)

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

## Enums |
|
|---|---|
Name |
Description |
`METADATA_SCHEMA_TYPE_UNSPECIFIED` |
Unspecified type for the MetadataSchema. |
`ARTIFACT_TYPE` |
A type indicating that the MetadataSchema will be used by Artifacts. |
`EXECUTION_TYPE` |
A typee indicating that the MetadataSchema will be used by Executions. |
`CONTEXT_TYPE` |
A state indicating that the MetadataSchema will be used by Contexts. |

## Methods

### MetadataSchemaType

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetVersionRequest -->

# Class DeleteDatasetVersionRequest (1.134.0)

`DeleteDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|

## Methods

### DeleteDatasetVersionRequest

`DeleteDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDatasetVersion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessSpec -->

# Class SummarizationHelpfulnessSpec (1.134.0)

```
SummarizationHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute summarization helpfulness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SummarizationHelpfulnessSpec

```
SummarizationHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager -->

# Class ListNotebookRuntimeTemplatesPager (1.134.0)

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimeTemplatesPager

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest -->

# Class ListPipelineJobsRequest (1.134.0)

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the PipelineJobs that match the filter expression. The following fields are supported: - `pipeline_name` : Supports `=` and `!=` comparisons.
- `display_name` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `pipeline_job_user_id` : Supports `=` , `!=`
comparisons, and `:` wildcard. for example, can check if
pipeline's display_name contains *step* by doing
display_name:"*step*"
- `state` : Supports `=` and `!=` comparisons.
- `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `end_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
- `template_uri` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `template_metadata.version` : Supports `=` , `!=`
comparisons, and `:` wildcard.
Filter expressions can be combined together using logical
operators (`AND` & `OR` ). For example:
`pipeline_name="test" AND create_time>"2020-05-18T13:30:00Z"` .
The syntax to define filter expression is based on
https://google.aip.dev/160.
Examples:
- `create_time>"2021-05-18T00:00:00Z" OR update_time>"2020-05-18T00:00:00Z"`
PipelineJobs created or updated after 2020-05-18 00:00:00
UTC.
- `labels.env = "prod"` PipelineJobs with label "env" set
to "prod".
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListPipelineJobsResponse.next_page_token of the previous PipelineService.ListPipelineJobs call. |
`order_by` |
`str`
A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple order_by fields provided e.g. "create_time desc, end_time", "end_time, start_time, update_time" For example, using "create_time desc, end_time" will order results by create time in descending order, and if there are multiple jobs having the same create time, order them by the end time in ascending order. if order_by is not specified, it will order by default order is create time in descending order. Supported fields: - `create_time`
- `update_time`
- `end_time`
- `start_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListPipelineJobsRequest

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringRelevanceInstance -->

# Class QuestionAnsweringRelevanceInstance (1.134.0)

```
QuestionAnsweringRelevanceInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance instance.

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
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringRelevanceInstance

```
QuestionAnsweringRelevanceInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Presets -->

# Class Presets (1.134.0)

`Presets(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Preset configuration for example-based explanations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`query` |
Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .
This field is a member of `oneof` _ `_query` .
|
`modality` |
The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type. |

## Classes

### Modality

`Modality(value)`


Preset option controlling parameters for different modalities

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Methods

### Presets

`Presets(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Preset configuration for example-based explanations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient -->

# Class EvaluationServiceAsyncClient (1.134.0)

```
EvaluationServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### EvaluationServiceAsyncClient

```
EvaluationServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the evaluation service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the EvaluationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### evaluate_instances

```
evaluate_instances(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.evaluation_service.EvaluateInstancesRequest,
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
) -> google.cloud.aiplatform_v1.types.evaluation_service.EvaluateInstancesResponse
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
from google.cloud import aiplatform_v1
async def sample_evaluate_instances():
# Create a client
client = aiplatform_v1.
```[EvaluationServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[EvaluateInstancesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesRequest.html)(
location="location_value",
)
# Make the request
response = await client.[evaluate_instances](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.evaluation_service.EvaluationServiceAsyncClient.html#google_cloud_aiplatform_v1_services_evaluation_service_EvaluationServiceAsyncClient_evaluate_instances)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EvaluationService.EvaluateInstances. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
`EvaluationServiceAsyncClient` |
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
`EvaluationServiceAsyncClient` |
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
`EvaluationServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.evaluation_service.transports.base.EvaluationServiceTransport
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookExecutionJobRequest -->

# Class GetNotebookExecutionJobRequest (1.134.0)

```
GetNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.GetNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource. |
`view` |
Optional. The NotebookExecutionJob view. Defaults to BASIC. |

## Methods

### GetNotebookExecutionJobRequest

```
GetNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.GetNotebookExecutionJob]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTuningJobsResponse -->

# Class ListTuningJobsResponse (1.134.0)

`ListTuningJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for GenAiTuningService.ListTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`tuning_jobs` |
`MutableSequence[`
List of TuningJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListTuningJobsResponse

`ListTuningJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for GenAiTuningService.ListTuningJobs

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse -->

# Class ListDatasetVersionsResponse (1.134.0)

`ListDatasetVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListDatasetVersions.

## Attributes |
|
|---|---|
Name |
Description |
`dataset_versions` |
`MutableSequence[`
A list of DatasetVersions that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListDatasetVersionsResponse

`ListDatasetVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListDatasetVersions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.Status -->

# Class Status (1.134.0)

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

## Attributes |
|
|---|---|
Name |
Description |
`message` |
`str`
Output only. The latest deployed model's status message (if any). |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The time at which the status was last updated. |
`available_replica_count` |
`int`
Output only. The number of available replicas of the deployed model. |

## Methods

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeechConfig -->

# Class SpeechConfig (1.134.0)

`SpeechConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for speech generation.

## Attributes |
|
|---|---|
Name |
Description |
`voice_config` |
The configuration for the voice to use. |
`language_code` |
`str`
Optional. The language code (ISO 639-1) for the speech synthesis. |
`multi_speaker_voice_config` |
The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` .
|

## Methods

### SpeechConfig

`SpeechConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for speech generation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.FeatureRegistrySource.FeatureGroup -->

# Class FeatureGroup (1.134.0)

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group_id` |
`str`
Required. Identifier of the feature group. |
`feature_ids` |
`MutableSequence[str]`
Required. Identifiers of features under the feature group. |

## Methods

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.StringFilter -->

# Class StringFilter (1.134.0)

`StringFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


String filter is used to search a subset of the entities by using boolean rules on string columns. For example: if a query specifies string filter with 'name = color, allow_tokens = {red, blue}, deny_tokens = {purple}',' then that query will match entities that are red or blue, but if those points are also purple, then they will be excluded even if they are red/blue. Only string filter is supported for now, numeric filter will be supported in the near future.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Column names in BigQuery that used as filters. |
`allow_tokens` |
`MutableSequence[str]`
Optional. The allowed tokens. |
`deny_tokens` |
`MutableSequence[str]`
Optional. The denied tokens. |

## Methods

### StringFilter

`StringFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


String filter is used to search a subset of the entities by using boolean rules on string columns. For example: if a query specifies string filter with 'name = color, allow_tokens = {red, blue}, deny_tokens = {purple}',' then that query will match entities that are red or blue, but if those points are also purple, then they will be excluded even if they are red/blue. Only string filter is supported for now, numeric filter will be supported in the near future.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest -->

# Class ListFeaturesRequest (1.134.0)

`ListFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list Features. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`filter` |
`str`
Lists the Features that match the filter expression. The following filters are supported: - `value_type` : Supports = and != comparisons.
- `create_time` : Supports =, !=, <,>, >=, and <= comparisons.="" values="" must="" be="" in="" rfc="" 3339="" format.="" -="">`update_time` : Supports =, !=, <,>, >=, and <= comparisons.="" values="" must="" be="" in="" rfc="" 3339="" format.="" -="">`labels` : Supports key-value equality as well as key
presence.
Examples:
- `value_type = DOUBLE` --> Features whose type is DOUBLE.
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` --> Features
having both (active: yes) and (env: prod) labels.
- `labels.env: *` --> Any Feature which has a label with
'env' as the key.
|
`page_size` |
`int`
The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 1000 Features will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListFeatures call or FeatureRegistryService.ListFeatures call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListFeatures or FeatureRegistryService.ListFeatures must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `feature_id`
- `value_type` (Not supported for FeatureRegistry Feature)
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`latest_stats_count` |
`int`
Only applicable for Vertex AI Feature Store (Legacy). If set, return the most recent ListFeaturesRequest.latest_stats_count of stats for each Feature in response. Valid value is [0, 10]. If number of stats exists <>ListFeaturesRequest.latest_stats_count, return all existing stats. |

## Methods

### ListFeaturesRequest

`ListFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringStatsPager -->

# Class SearchModelMonitoringStatsPager (1.134.0)

```
SearchModelMonitoringStatsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
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


A pager for iterating through `search_model_monitoring_stats`

requests.

This class thinly wraps an initial
[SearchModelMonitoringStatsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelMonitoringStats`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelMonitoringStatsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelMonitoringStatsPager

```
SearchModelMonitoringStatsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsOperationMetadata -->

# Class BatchCancelPipelineJobsOperationMetadata (1.134.0)

```
BatchCancelPipelineJobsOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for PipelineService.BatchCancelPipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### BatchCancelPipelineJobsOperationMetadata

```
BatchCancelPipelineJobsOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.IntValueCondition -->

# Class IntValueCondition (1.134.0)

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[int]`
Required. Matches values of the parent parameter of 'INTEGER' type. All values must lie in `integer_value_spec` of parent parameter.
|

## Methods

### IntValueCondition

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse -->

# Class ListCachedContentsResponse (1.134.0)

`ListCachedContentsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response with a list of CachedContents.

## Attributes |
|
|---|---|
Name |
Description |
`cached_contents` |
`MutableSequence[`
List of cached contents. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|

## Methods

### ListCachedContentsResponse

`ListCachedContentsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response with a list of CachedContents.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BleuSpec -->

# Class BleuSpec (1.134.0)

`BleuSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

## Attribute |
|
|---|---|
Name |
Description |
`use_effective_order` |
`bool`
Optional. Whether to use_effective_order to compute bleu score. |

## Methods

### BleuSpec

`BleuSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.RetrievedContext -->

# Class RetrievedContext (1.134.0)

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_chunk` |
Additional context for the RAG retrieval result. This is only populated when using the RAG retrieval tool. This field is a member of `oneof` _ `context_details` .
|
`uri` |
`str`
URI reference of the attribution. This field is a member of `oneof` _ `_uri` .
|
`title` |
`str`
Title of the attribution. This field is a member of `oneof` _ `_title` .
|
`text` |
`str`
Text of the attribution. This field is a member of `oneof` _ `_text` .
|
`document_name` |
`str`
Output only. The full document name for the referenced Vertex AI Search document. This field is a member of `oneof` _ `_document_name` .
|

## Methods

### RetrievedContext

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec -->

# Class MultiTrialAlgorithmSpec (1.134.0)

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm` |
The multi-trial Neural Architecture Search (NAS) algorithm type. Defaults to `REINFORCEMENT_LEARNING` .
|
`metric` |
Metric specs for the NAS job. Validation for this field is done at `multi_trial_algorithm_spec` field.
|
`search_trial_spec` |
Required. Spec for search trials. |
`train_trial_spec` |
Spec for train trials. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Classes

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

### MultiTrialAlgorithm

`MultiTrialAlgorithm(value)`


The available types of multi-trial algorithms.

### SearchTrialSpec

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Methods

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModelView -->

# Class PublisherModelView (1.134.0)

`PublisherModelView(value)`


View enumeration of PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`PUBLISHER_MODEL_VIEW_UNSPECIFIED` |
The default / unset value. The API will default to the BASIC view. |
`PUBLISHER_MODEL_VIEW_BASIC` |
Include basic metadata about the publisher model, but not the full contents. |
`PUBLISHER_MODEL_VIEW_FULL` |
Include everything. |
`PUBLISHER_MODEL_VERSION_VIEW_BASIC` |
Include: VersionId, ModelVersionExternalName, and SupportedActions. |

## Methods

### PublisherModelView

`PublisherModelView(value)`


View enumeration of PublisherModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetOperationMetadata -->

# Class UpdateExplanationDatasetOperationMetadata (1.134.0)

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateExplanationDatasetOperationMetadata

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Presets -->

# Class Presets (1.134.0)

`Presets(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Preset configuration for example-based explanations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`query` |
Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .
This field is a member of `oneof` _ `_query` .
|
`modality` |
The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type. |

## Classes

### Modality

`Modality(value)`


Preset option controlling parameters for different modalities

### Query

`Query(value)`


Preset option controlling parameters for query speed-precision trade-off

## Methods

### Presets

`Presets(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Preset configuration for example-based explanations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery -->

# Class RagQuery (1.134.0)

`RagQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to retrieve relevant contexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`text` |
`str`
Optional. The query in text format to get relevant contexts. This field is a member of `oneof` _ `query` .
|
`similarity_top_k` |
`int`
Optional. The number of contexts to retrieve. |
`ranking` |
Optional. Configurations for hybrid search results ranking. |
`rag_retrieval_config` |
Optional. The retrieval config for the query. |

## Classes

### Ranking

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for hybrid search results ranking.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagQuery

`RagQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to retrieve relevant contexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CodeExecutionResult.Outcome -->

# Class Outcome (1.134.0)

`Outcome(value)`


Enumeration of possible outcomes of the code execution.

## Enums |
|
|---|---|
Name |
Description |
`OUTCOME_UNSPECIFIED` |
Unspecified status. This value should not be used. |
`OUTCOME_OK` |
Code execution completed successfully. |
`OUTCOME_FAILED` |
Code execution finished but with a failure. `stderr` should contain the reason. |
`OUTCOME_DEADLINE_EXCEEDED` |
Code execution ran for too long, and was cancelled. There may or may not be a partial output present. |

## Methods

### Outcome

`Outcome(value)`


Enumeration of possible outcomes of the code execution.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse -->

# Class ListStudiesResponse (1.134.0)

`ListStudiesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`studies` |
`MutableSequence[`
The studies associated with the project. |
`next_page_token` |
`str`
Passes this token as the `page_token` field of the request
for a subsequent call. If this field is omitted, there are
no subsequent pages.
|

## Methods

### ListStudiesResponse

`ListStudiesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListStudies.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient -->

# Class DataFoundryServiceClient (1.134.0)

```
DataFoundryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for generating and preparing datasets for Gen AI evaluation.

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
`DataFoundryServiceTransport` |
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

### DataFoundryServiceClient

```
DataFoundryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the data foundry service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DataFoundryServiceTransport,Callable[..., DataFoundryServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the DataFoundryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`DataFoundryServiceClient` |
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
`DataFoundryServiceClient` |
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
`DataFoundryServiceClient` |
The constructed client. |

### generate_synthetic_data

```
generate_synthetic_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.data_foundry_service.GenerateSyntheticDataRequest,
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
google.cloud.aiplatform_v1.types.data_foundry_service.GenerateSyntheticDataResponse
)
```


Generates synthetic data based on the provided configuration.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_generate_synthetic_data():
# Create a client
client = aiplatform_v1.
```[DataFoundryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient.html)()
# Initialize request argument(s)
task_description = aiplatform_v1.[TaskDescriptionStrategy](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TaskDescriptionStrategy.html)()
task_description.task_description = "task_description_value"
output_field_specs = aiplatform_v1.[OutputFieldSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.OutputFieldSpec.html)()
output_field_specs.field_name = "field_name_value"
request = aiplatform_v1.[GenerateSyntheticDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataRequest.html)(
task_description=task_description,
location="location_value",
count=553,
output_field_specs=output_field_specs,
)
# Make the request
response = client.[generate_synthetic_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceClient.html#google_cloud_aiplatform_v1_services_data_foundry_service_DataFoundryServiceClient_generate_synthetic_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DataFoundryService.GenerateSyntheticData. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
The response containing the generated data. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringRelevanceSpec -->

# Class QuestionAnsweringRelevanceSpec (1.134.0)

```
QuestionAnsweringRelevanceSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering relevance. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringRelevanceSpec

```
QuestionAnsweringRelevanceSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveDatapointsRequest -->

# Class RemoveDatapointsRequest (1.134.0)

`RemoveDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.RemoveDatapoints

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`str`
Required. The name of the Index resource to be updated. Format: `projects/{project}/locations/{location}/indexes/{index}`
|
`datapoint_ids` |
`MutableSequence[str]`
A list of datapoint ids to be deleted. |

## Methods

### RemoveDatapointsRequest

`RemoveDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.RemoveDatapoints

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceInstance -->

# Class QuestionAnsweringRelevanceInstance (1.134.0)

```
QuestionAnsweringRelevanceInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance instance.

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
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringRelevanceInstance

```
QuestionAnsweringRelevanceInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryRequest -->

# Class CreateMemoryRequest (1.134.0)

`CreateMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.CreateMemory.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to create the Memory under. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`memory` |
Required. The Memory to be created. |

## Methods

### CreateMemoryRequest

`CreateMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.CreateMemory.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.VertexRagStore.RagResource -->

# Class RagResource (1.134.0)

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpus` |
`str`
Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`rag_file_ids` |
`MutableSequence[str]`
Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field. |

## Methods

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Candidate.FinishReason -->

# Class FinishReason (1.134.0)

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

## Enums |
|
|---|---|
Name |
Description |
`FINISH_REASON_UNSPECIFIED` |
The finish reason is unspecified. |
`STOP` |
Token generation reached a natural stopping point or a configured stop sequence. |
`MAX_TOKENS` |
Token generation reached the configured maximum output tokens. |
`SAFETY` |
Token generation stopped because the content potentially contains safety violations. NOTE: When streaming, content is empty if content filters blocks the output. |
`RECITATION` |
Token generation stopped because the content potentially contains copyright violations. |
`OTHER` |
All other reasons that stopped the token generation. |
`BLOCKLIST` |
Token generation stopped because the content contains forbidden terms. |
`PROHIBITED_CONTENT` |
Token generation stopped for potentially containing prohibited content. |
`SPII` |
Token generation stopped because the content potentially contains Sensitive Personally Identifiable Information (SPII). |
`MALFORMED_FUNCTION_CALL` |
The function call generated by the model is invalid. |
`MODEL_ARMOR` |
The model response was blocked by Model Armor. |

## Methods

### FinishReason

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesOperationMetadata -->

# Class ImportFeatureValuesOperationMetadata (1.134.0)

```
ImportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform import Feature values.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore import Feature values. |
`imported_entity_count` |
`int`
Number of entities that have been imported by the operation. |
`imported_feature_value_count` |
`int`
Number of Feature values that have been imported by the operation. |
`source_uris` |
`MutableSequence[str]`
The source URI from where Feature values are imported. |
`invalid_row_count` |
`int`
The number of rows in input source that weren't imported due to either - Not having any featureValues. - Having a null entityId. - Having a null timestamp. - Not being parsable (applicable for CSV sources). |
`timestamp_outside_retention_rows_count` |
`int`
The number rows that weren't ingested due to having timestamps outside the retention boundary. |
`blocking_operation_ids` |
`MutableSequence[int]`
List of ImportFeatureValues operations running under a single EntityType that are blocking this operation. |

## Methods

### ImportFeatureValuesOperationMetadata

```
ImportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform import Feature values.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualitySpec -->

# Class QuestionAnsweringQualitySpec (1.134.0)

```
QuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality score metric.

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

### QuestionAnsweringQualitySpec

```
QuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ComputeTokensResponse -->

# Class ComputeTokensResponse (1.134.0)

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.

## Attribute |
|
|---|---|
Name |
Description |
`tokens_info` |
`MutableSequence[`
Lists of tokens info from the input. A ComputeTokensRequest could have multiple instances with a prompt in each instance. We also need to return lists of tokens info for the request with multiple instances. |

## Methods

### ComputeTokensResponse

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesAsyncPager -->

# Class ListTensorboardTimeSeriesAsyncPager (1.134.0)

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardTimeSeriesAsyncPager

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager -->

# Class ListHyperparameterTuningJobsAsyncPager (1.134.0)

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

## Methods

### ListHyperparameterTuningJobsAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTrainingPipelineRequest -->

# Class CancelTrainingPipelineRequest (1.134.0)

```
CancelTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CancelTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### CancelTrainingPipelineRequest

```
CancelTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CancelTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TokensInfo -->

# Class TokensInfo (1.134.0)

`TokensInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tokens info with a list of tokens and the corresponding list of token ids.

## Attributes |
|
|---|---|
Name |
Description |
`tokens` |
`MutableSequence[bytes]`
A list of tokens from the input. |
`token_ids` |
`MutableSequence[int]`
A list of token ids from the input. |
`role` |
`str`
Optional. Optional fields for the role from the corresponding Content. |

## Methods

### TokensInfo

`TokensInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tokens info with a list of tokens and the corresponding list of token ids.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardRequest -->

# Class CreateTensorboardRequest (1.134.0)

`CreateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.CreateTensorboard.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Tensorboard in. Format: `projects/{project}/locations/{location}`
|
`tensorboard` |
Required. The Tensorboard to create. |

## Methods

### CreateTensorboardRequest

`CreateTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.CreateTensorboard.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesRequest.FeatureSpec -->

# Class FeatureSpec (1.134.0)

`FeatureSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines the Feature value(s) to import.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Required. ID of the Feature to import values of. This Feature must exist in the target EntityType, or the request will fail. |
`source_field` |
`str`
Source column to get the Feature values from. If not set, uses the column with the same name as the Feature ID. |

## Methods

### FeatureSpec

`FeatureSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines the Feature value(s) to import.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.DeploymentSpec -->

# Class DeploymentSpec (1.134.0)

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`env` |
`MutableSequence[`
Optional. Environment variables to be set with the Reasoning Engine deployment. The environment variables can be updated through the UpdateReasoningEngine API. |
`secret_env` |
`MutableSequence[`
Optional. Environment variables where the value is a secret in Cloud Secret Manager. To use this feature, add 'Secret Manager Secret Accessor' role (roles/secretmanager.secretAccessor) to AI Platform Reasoning Engine Service Agent. |
`psc_interface_config` |
Optional. Configuration for PSC-I. |
`min_instances` |
`int`
Optional. The minimum number of application instances that will be kept running at all times. Defaults to 1. Range: [0, 10]. This field is a member of `oneof` _ `_min_instances` .
|
`max_instances` |
`int`
Optional. The maximum number of application instances that can be launched to handle increased traffic. Defaults to 100. Range: [1, 1000]. If VPC-SC or PSC-I is enabled, the acceptable range is [1, 100]. This field is a member of `oneof` _ `_max_instances` .
|
`resource_limits` |
`MutableMapping[str, str]`
Optional. Resource limits for each container. Only 'cpu' and 'memory' keys are supported. Defaults to {"cpu": "4", "memory": "4Gi"}. - The only supported values for CPU are '1', '2', '4', '6' and '8'. For more information, go to https://cloud.google.com/run/docs/configuring/cpu. - The only supported values for memory are '1Gi', '2Gi', ... '32 Gi'. - For required cpu on different memory values, go to https://cloud.google.com/run/docs/configuring/memory-limits |
`container_concurrency` |
`int`
Optional. Concurrency for each container and agent server. Recommended value: 2 \* cpu + 1. Defaults to 9. This field is a member of `oneof` _ `_container_concurrency` .
|

## Classes

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

## Methods

### DeploymentSpec

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk.RetrievedContext -->

# Class RetrievedContext (1.134.0)

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_chunk` |
Additional context for the RAG retrieval result. This is only populated when using the RAG retrieval tool. This field is a member of `oneof` _ `context_details` .
|
`uri` |
`str`
URI reference of the attribution. This field is a member of `oneof` _ `_uri` .
|
`title` |
`str`
Title of the attribution. This field is a member of `oneof` _ `_title` .
|
`text` |
`str`
Text of the attribution. This field is a member of `oneof` _ `_text` .
|
`document_name` |
`str`
Output only. The full document name for the referenced Vertex AI Search document. This field is a member of `oneof` _ `_document_name` .
|

## Methods

### RetrievedContext

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation -->

# Class NumericArrayTransformation (1.134.0)

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationSlicesAsyncPager -->

# Class ListModelEvaluationSlicesAsyncPager (1.134.0)

```
ListModelEvaluationSlicesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse,
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


A pager for iterating through `list_model_evaluation_slices`

requests.

This class thinly wraps an initial
[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_evaluation_slices`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelEvaluationSlices`

requests and continue to iterate
through the `model_evaluation_slices`

field on the
corresponding responses.

All the usual [ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationSlicesAsyncPager

```
ListModelEvaluationSlicesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager -->

# Class ListModelDeploymentMonitoringJobsPager (1.134.0)

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

## Methods

### ListModelDeploymentMonitoringJobsPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileMetadataConfig -->

# Class RagFileMetadataConfig (1.134.0)

`RagFileMetadataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata config for RagFile.

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
`gcs_metadata_schema_source` |
Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucket_name/my_directory/object_name/metadata_schema.json`
- `gs://bucket_name/my_directory` If the user provides a
directory, the metadata schema will be read from the files
that ends with "metadata_schema.json" in the directory.
This field is a member of `oneof` _ `metadata_schema_source` .
|
`google_drive_metadata_schema_source` |
Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a folder, the metadata schema will be read from the files that ends with "metadata_schema.json" in the directory. This field is a member of `oneof` _ `metadata_schema_source` .
|
`inline_metadata_schema_source` |
`str`
Inline metadata schema source. Must be a JSON string. This field is a member of `oneof` _ `metadata_schema_source` .
|
`gcs_metadata_source` |
Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucket_name/my_directory/object_name/metadata.json`
- `gs://bucket_name/my_directory` If the user provides a
directory, the metadata will be read from the files that
ends with "metadata.json" in the directory.
This field is a member of `oneof` _ `metadata_source` .
|
`google_drive_metadata_source` |
Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a directory, the metadata will be read from the files that ends with "metadata.json" in the directory. This field is a member of `oneof` _ `metadata_source` .
|
`inline_metadata_source` |
`str`
Inline metadata source. Must be a JSON string. This field is a member of `oneof` _ `metadata_source` .
|

## Methods

### RagFileMetadataConfig

`RagFileMetadataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata config for RagFile.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial -->

# Class Trial (1.134.0)

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Trial assigned by the service. |
`id` |
`str`
Output only. The identifier of the Trial assigned by the service. |
`state` |
Output only. The detailed state of the Trial. |
`parameters` |
`MutableSequence[`
Output only. The parameters of the Trial. |
`final_measurement` |
Output only. The final measurement containing the objective value. |
`measurements` |
`MutableSequence[`
Output only. A list of measurements that are strictly lexicographically ordered by their induced tuples (steps, elapsed_duration). These are used for early stopping computations. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial's status changed to `SUCCEEDED` or `INFEASIBLE` .
|
`client_id` |
`str`
Output only. The identifier of the client that originally requested this Trial. Each client is identified by a unique client_id. When a client asks for a suggestion, Vertex AI Vizier will assign it a Trial. The client should evaluate the Trial, complete it, and report back to Vertex AI Vizier. If suggestion is asked again by same client_id before the Trial is completed, the same Trial will be returned. Multiple clients with different client_ids can ask for suggestions simultaneously, each of them will get their own Trial. |
`infeasible_reason` |
`str`
Output only. A human readable string describing why the Trial is infeasible. This is set only if Trial state is `INFEASIBLE` .
|
`custom_job` |
`str`
Output only. The CustomJob name linked to the Trial. It's set for a HyperparameterTuningJob's Trial. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |

## Classes

### Parameter

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

### State

`State(value)`


Describes a Trial state.

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

### Trial

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact -->

# Class Artifact (1.134.0)

```
Artifact(
artifact_name: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
)
```


Metadata Artifact resource for Vertex AI

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

### lineage_console_uri

Cloud console uri to view this Artifact Lineage.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### state

The State for this Artifact.

### update_time

Time this resource was last updated.

### uri

Uri for this Artifact.

## Methods

### Artifact

```
Artifact(
artifact_name: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
)
```


Retrieves an existing Metadata Artifact given a resource name or ID.

Parameters |
|
|---|---|
Name |
Description |
`artifact_name` |
`str`
Required. A fully-qualified resource name or resource ID of the Artifact. Example: "projects/123/locations/us-central1/metadataStores/default/artifacts/my-resource". or "my-resource" when project and location are initialized or passed. |
`metadata_store_id` |
`str`
Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_name is a fully-qualified resource, its metadata_store_id overrides this one. |
`project` |
`str`
Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

### create

```
create(
schema_title: str,
*,
resource_id: typing.Optional[str] = None,
uri: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
state: google.cloud.aiplatform_v1.types.artifact.Artifact.State = State.LIVE,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.artifact.Artifact
```


Creates a new Metadata Artifact.

Parameters |
|
|---|---|
Name |
Description |
`schema_title` |
`str`
Required. schema_title identifies the schema title used by the Artifact. Please reference |
`resource_id` |
`str`
Optional. The <resource_id> portion of the Artifact name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id>. |
`uri` |
`str`
Optional. The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file. |
`display_name` |
`str`
Optional. The user-defined name of the Artifact. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the Artifact. If not set, defaults to use the latest version. |
`description` |
`str`
Optional. Describes the purpose of the Artifact to be created. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the Artifact. |
`state` |
`google.cloud.gapic.types.Artifact.State`
Optional. The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |
`metadata_store_id` |
`str`
Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Optional. Project used to create this Artifact. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location used to create this Artifact. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials used to create this Artifact. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`Artifact` |
Instantiated representation of the managed Metadata Artifact. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### get

```
get(
resource_id: str,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.metadata.resource._Resource
```


Retrieves a Metadata resource.

Parameters |
|
|---|---|
Name |
Description |
`resource_id` |
`str`
Required. The <resource_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id>. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to retrieve or create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to retrieve or create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to retrieve or create this resource. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`resource (_Resource)` |
Instantiated representation of the managed Metadata resource or None if no resource was found. |

### get_or_create

```
get_or_create(
resource_id: str,
schema_title: str,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.metadata.resource._Resource
```


Retrieves or Creates (if it does not exist) a Metadata resource.

Parameters |
|
|---|---|
Name |
Description |
`resource_id` |
`str`
Required. The <resource_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id>. |
`schema_title` |
`str`
Required. schema_title identifies the schema title used by the resource. |
`display_name` |
`str`
Optional. The user-defined name of the resource. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the resource. If not set, defaults to use the latest version. |
`description` |
`str`
Optional. Describes the purpose of the resource to be created. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the resource. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to retrieve or create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to retrieve or create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to retrieve or create this resource. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`resource (_Resource)` |
Instantiated representation of the managed Metadata resource. |

### get_with_uri

```
get_with_uri(
uri: str,
*,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.artifact.Artifact
```


Get an Artifact by it's uri.

If more than one Artifact with this uri is in the metadata store then the Artifact with the latest create_time is returned.

Parameters |
|
|---|---|
Name |
Description |
`uri` |
`str`
Required. Uri of the Artifact to retrieve. |
`metadata_store_id` |
`str`
Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_name is a fully-qualified resource, its metadata_store_id overrides this one. |
`project` |
`str`
Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If no Artifact exists with the provided uri. |

Returns |
|
|---|---|
Type |
Description |
`Artifact` |
Artifact with given uri. |

### list

```
list(
filter: typing.Optional[str] = None,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
order_by: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.metadata.resource._Resource]
```


List resources that match the list filter in target metadataStore.

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. A query to filter available resources for matching results. |
`metadata_store_id` |
`str`
The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/<resource_noun>/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str`
Project used to create this resource. Overrides project set in aiplatform.init. |
`location` |
`str`
Location used to create this resource. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials used to create this resource. Overrides credentials set in aiplatform.init. |
`order_by` |
`str`
Optional. How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a |

Returns |
|
|---|---|
Type |
Description |
`resources (sequence[_Resource])` |
a list of managed Metadata resource. |

### sync_resource

`sync_resource()`


Syncs local resource with the resource in metadata store.

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
metadata: typing.Optional[typing.Dict] = None,
description: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
location: typing.Optional[str] = None,
)
```


Updates an existing Metadata resource with new metadata.

Parameters |
|
|---|---|
Name |
Description |
`metadata` |
`Dict`
Optional. metadata contains the updated metadata information. |
`description` |
`str`
Optional. Description describes the resource to be updated. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to update this resource. Overrides credentials set in aiplatform.init. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDeploymentResourcePoolOperationMetadata -->

# Class UpdateDeploymentResourcePoolOperationMetadata (1.134.0)

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateDeploymentResourcePoolOperationMetadata

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolOperationMetadata -->

# Class CreateDeploymentResourcePoolOperationMetadata (1.134.0)

```
CreateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for CreateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDeploymentResourcePoolOperationMetadata

```
CreateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for CreateDeploymentResourcePool method.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataSchema.MetadataSchemaType -->

# Class MetadataSchemaType (1.134.0)

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

## Enums |
|
|---|---|
Name |
Description |
`METADATA_SCHEMA_TYPE_UNSPECIFIED` |
Unspecified type for the MetadataSchema. |
`ARTIFACT_TYPE` |
A type indicating that the MetadataSchema will be used by Artifacts. |
`EXECUTION_TYPE` |
A typee indicating that the MetadataSchema will be used by Executions. |
`CONTEXT_TYPE` |
A state indicating that the MetadataSchema will be used by Contexts. |

## Methods

### MetadataSchemaType

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse -->

# Class ListTuningJobsResponse (1.134.0)

`ListTuningJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for GenAiTuningService.ListTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`tuning_jobs` |
`MutableSequence[`
List of TuningJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListTuningJobsResponse

`ListTuningJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for GenAiTuningService.ListTuningJobs

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeechConfig -->

# Class SpeechConfig (1.134.0)

`SpeechConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for speech generation.

## Attributes |
|
|---|---|
Name |
Description |
`voice_config` |
The configuration for the voice to use. |
`language_code` |
`str`
Optional. The language code (ISO 639-1) for the speech synthesis. |
`multi_speaker_voice_config` |
The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` .
|

## Methods

### SpeechConfig

`SpeechConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for speech generation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IdMatcher -->

# Class IdMatcher (1.134.0)

`IdMatcher(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Matcher for Features of an EntityType by Feature ID.

## Attribute |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[str]`
Required. The following are accepted as `ids` :
- A single-element list containing only `*` , which selects
all Features in the target EntityType, or
- A list containing only Feature IDs, which selects only
Features with those IDs in the target EntityType.
|

## Methods

### IdMatcher

`IdMatcher(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Matcher for Features of an EntityType by Feature ID.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookExecutionJobRequest -->

# Class GetNotebookExecutionJobRequest (1.134.0)

```
GetNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.GetNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookExecutionJob resource. |
`view` |
Optional. The NotebookExecutionJob view. Defaults to BASIC. |

## Methods

### GetNotebookExecutionJobRequest

```
GetNotebookExecutionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [NotebookService.GetNotebookExecutionJob]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SyncFeatureViewResponse -->

# Class SyncFeatureViewResponse (1.134.0)

`SyncFeatureViewResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.SyncFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`feature_view_sync` |
`str`
Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### SyncFeatureViewResponse

`SyncFeatureViewResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.SyncFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.RecordError.RecordErrorType -->

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

Methods

RecordErrorType

RecordErrorType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Candidate.FinishReason -->

# Class FinishReason (1.134.0)

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

## Enums |
|
|---|---|
Name |
Description |
`FINISH_REASON_UNSPECIFIED` |
The finish reason is unspecified. |
`STOP` |
Token generation reached a natural stopping point or a configured stop sequence. |
`MAX_TOKENS` |
Token generation reached the configured maximum output tokens. |
`SAFETY` |
Token generation stopped because the content potentially contains safety violations. NOTE: When streaming, content is empty if content filters blocks the output. |
`RECITATION` |
Token generation stopped because the content potentially contains copyright violations. |
`OTHER` |
All other reasons that stopped the token generation. |
`BLOCKLIST` |
Token generation stopped because the content contains forbidden terms. |
`PROHIBITED_CONTENT` |
Token generation stopped for potentially containing prohibited content. |
`SPII` |
Token generation stopped because the content potentially contains Sensitive Personally Identifiable Information (SPII). |
`MALFORMED_FUNCTION_CALL` |
The function call generated by the model is invalid. |
`MODEL_ARMOR` |
The model response was blocked by Model Armor. |

## Methods

### FinishReason

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.DeploymentSpec -->

# Class DeploymentSpec (1.134.0)

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`env` |
`MutableSequence[`
Optional. Environment variables to be set with the Reasoning Engine deployment. The environment variables can be updated through the UpdateReasoningEngine API. |
`secret_env` |
`MutableSequence[`
Optional. Environment variables where the value is a secret in Cloud Secret Manager. To use this feature, add 'Secret Manager Secret Accessor' role (roles/secretmanager.secretAccessor) to AI Platform Reasoning Engine Service Agent. |
`psc_interface_config` |
Optional. Configuration for PSC-I. |
`min_instances` |
`int`
Optional. The minimum number of application instances that will be kept running at all times. Defaults to 1. Range: [0, 10]. This field is a member of `oneof` _ `_min_instances` .
|
`max_instances` |
`int`
Optional. The maximum number of application instances that can be launched to handle increased traffic. Defaults to 100. Range: [1, 1000]. If VPC-SC or PSC-I is enabled, the acceptable range is [1, 100]. This field is a member of `oneof` _ `_max_instances` .
|
`resource_limits` |
`MutableMapping[str, str]`
Optional. Resource limits for each container. Only 'cpu' and 'memory' keys are supported. Defaults to {"cpu": "4", "memory": "4Gi"}. - The only supported values for CPU are '1', '2', '4', '6' and '8'. For more information, go to https://cloud.google.com/run/docs/configuring/cpu. - The only supported values for memory are '1Gi', '2Gi', ... '32 Gi'. - For required cpu on different memory values, go to https://cloud.google.com/run/docs/configuring/memory-limits |
`container_concurrency` |
`int`
Optional. Concurrency for each container and agent server. Recommended value: 2 \* cpu + 1. Defaults to 9. This field is a member of `oneof` _ `_container_concurrency` .
|

## Classes

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

## Methods

### DeploymentSpec

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataPager -->

# Class ExportTensorboardTimeSeriesDataPager (1.134.0)

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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


A pager for iterating through `export_tensorboard_time_series_data`

requests.

This class thinly wraps an initial
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse) object, and
provides an `__iter__`

method to iterate through its
`time_series_data_points`

field.

If there are more pages, the `__iter__`

method will make additional
`ExportTensorboardTimeSeriesData`

requests and continue to iterate
through the `time_series_data_points`

field on the
corresponding responses.

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ExportTensorboardTimeSeriesDataPager

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesOperationMetadata -->

# Class ImportFeatureValuesOperationMetadata (1.134.0)

```
ImportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform import Feature values.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore import Feature values. |
`imported_entity_count` |
`int`
Number of entities that have been imported by the operation. |
`imported_feature_value_count` |
`int`
Number of Feature values that have been imported by the operation. |
`source_uris` |
`MutableSequence[str]`
The source URI from where Feature values are imported. |
`invalid_row_count` |
`int`
The number of rows in input source that weren't imported due to either - Not having any featureValues. - Having a null entityId. - Having a null timestamp. - Not being parsable (applicable for CSV sources). |
`timestamp_outside_retention_rows_count` |
`int`
The number rows that weren't ingested due to having timestamps outside the retention boundary. |
`blocking_operation_ids` |
`MutableSequence[int]`
List of ImportFeatureValues operations running under a single EntityType that are blocking this operation. |

## Methods

### ImportFeatureValuesOperationMetadata

```
ImportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform import Feature values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringAlertConfig -->

# Class ModelMonitoringAlertConfig (1.134.0)

`ModelMonitoringAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The alert config for model monitoring.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`email_alert_config` |
Email alert config. This field is a member of `oneof` _ `alert` .
|
`enable_logging` |
`bool`
Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto ModelMonitoringStatsAnomalies. This can be further synced to Pub/Sub or any other services supported by Cloud Logging. |
`notification_channels` |
`MutableSequence[str]`
Resource names of the NotificationChannels to send alert. Must be of the format `projects/`
|

## Classes

### EmailAlertConfig

`EmailAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for email alert.

## Methods

### ModelMonitoringAlertConfig

`ModelMonitoringAlertConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The alert config for model monitoring.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsAsyncPager -->

# Class ListFeatureViewSyncsAsyncPager (1.134.0)

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewSyncsAsyncPager

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial -->

# Class Trial (1.134.0)

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Trial assigned by the service. |
`id` |
`str`
Output only. The identifier of the Trial assigned by the service. |
`state` |
Output only. The detailed state of the Trial. |
`parameters` |
`MutableSequence[`
Output only. The parameters of the Trial. |
`final_measurement` |
Output only. The final measurement containing the objective value. |
`measurements` |
`MutableSequence[`
Output only. A list of measurements that are strictly lexicographically ordered by their induced tuples (steps, elapsed_duration). These are used for early stopping computations. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial's status changed to `SUCCEEDED` or `INFEASIBLE` .
|
`client_id` |
`str`
Output only. The identifier of the client that originally requested this Trial. Each client is identified by a unique client_id. When a client asks for a suggestion, Vertex AI Vizier will assign it a Trial. The client should evaluate the Trial, complete it, and report back to Vertex AI Vizier. If suggestion is asked again by same client_id before the Trial is completed, the same Trial will be returned. Multiple clients with different client_ids can ask for suggestions simultaneously, each of them will get their own Trial. |
`infeasible_reason` |
`str`
Output only. A human readable string describing why the Trial is infeasible. This is set only if Trial state is `INFEASIBLE` .
|
`custom_job` |
`str`
Output only. The CustomJob name linked to the Trial. It's set for a HyperparameterTuningJob's Trial. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |

## Classes

### Parameter

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

### State

`State(value)`


Describes a Trial state.

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

### Trial

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelView -->

# Class PublisherModelView (1.134.0)

`PublisherModelView(value)`


View enumeration of PublisherModel.

## Enums |
|
|---|---|
Name |
Description |
`PUBLISHER_MODEL_VIEW_UNSPECIFIED` |
The default / unset value. The API will default to the BASIC view. |
`PUBLISHER_MODEL_VIEW_BASIC` |
Include basic metadata about the publisher model, but not the full contents. |
`PUBLISHER_MODEL_VIEW_FULL` |
Include everything. |
`PUBLISHER_MODEL_VERSION_VIEW_BASIC` |
Include: VersionId, ModelVersionExternalName, and SupportedActions. |

## Methods

### PublisherModelView

`PublisherModelView(value)`


View enumeration of PublisherModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.Status -->

# Class Status (1.134.0)

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

## Attributes |
|
|---|---|
Name |
Description |
`message` |
`str`
Output only. The latest deployed model's status message (if any). |
`last_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The time at which the status was last updated. |
`available_replica_count` |
`int`
Output only. The number of available replicas of the deployed model. |

## Methods

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service -->

# Package specialist_pool_service (1.134.0)

API documentation for `aiplatform_v1.services.specialist_pool_service`

package.

## Classes

[SpecialistPoolServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient)

A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

[SpecialistPoolServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.SpecialistPoolServiceClient)

A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers)

API documentation for `aiplatform_v1.services.specialist_pool_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.IntValueCondition -->

# Class IntValueCondition (1.134.0)

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[int]`
Required. Matches values of the parent parameter of 'INTEGER' type. All values must lie in `integer_value_spec` of parent parameter.
|

## Methods

### IntValueCondition

`IntValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match integer values from parent parameter.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse -->

# Class ListRagCorporaResponse (1.134.0)

`ListRagCorporaResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagCorpora.

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpora` |
`MutableSequence[`
List of RagCorpora in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListRagCorporaRequest.page_token to obtain that page. |

## Methods

### ListRagCorporaResponse

`ListRagCorporaResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagCorpora.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringHelpfulnessInstance -->

# Class QuestionAnsweringHelpfulnessInstance (1.134.0)

```
QuestionAnsweringHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness instance.

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
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringHelpfulnessInstance

```
QuestionAnsweringHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex -->

# Class DeployedIndex (1.134.0)

`DeployedIndex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Required. The user specified ID of the DeployedIndex. The ID can be up to 128 characters long and must start with a letter and only contain letters, numbers, and underscores. The ID must be unique within the project it is created in. |
`index` |
`str`
Required. The name of the Index this is the deployment of. We may refer to this Index as the DeployedIndex's "original" Index. |
`display_name` |
`str`
The display name of the DeployedIndex. If not provided upon creation, the Index's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedIndex was created. |
`private_endpoints` |
Output only. Provides paths for users to send requests directly to the deployed index services running on Cloud via private services access. This field is populated if network is configured. |
`index_sync_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The DeployedIndex may depend on various data on its original Index. Additionally when certain changes to the original Index are being done (e.g. when what the Index contains is being changed) the DeployedIndex may be asynchronously updated in the background to reflect these changes. If this timestamp's value is at least the Index.update_time of the original Index, it means that this DeployedIndex and the original Index are in sync. If this timestamp is older, then to see which updates this DeployedIndex already contains (and which it does not), one must `list][google.longrunning.Operations.ListOperations]` the
operations that are running on the original Index. Only the
successfully completed Operations with
update_time
equal or before this sync time are contained in this
DeployedIndex.
|
`automatic_resources` |
Optional. A description of resources that the DeployedIndex uses, which to large degree are decided by Vertex AI, and optionally allows only a modest additional configuration. If min_replica_count is not set, the default value is 2 (we don't provide SLA when min_replica_count=1). If max_replica_count is not set, the default value is min_replica_count. The max allowed replica count is 1000. |
`dedicated_resources` |
Optional. A description of resources that are dedicated to the DeployedIndex, and that need a higher degree of manual configuration. The field min_replica_count must be set to a value strictly greater than 0, or else validation will fail. We don't provide SLA when min_replica_count=1. If max_replica_count is not set, the default value is min_replica_count. The max allowed replica count is 1000. Available machine types for SMALL shard: e2-standard-2 and all machine types available for MEDIUM and LARGE shard. Available machine types for MEDIUM shard: e2-standard-16 and all machine types available for LARGE shard. Available machine types for LARGE shard: e2-highmem-16, n2d-standard-32. n1-standard-16 and n1-standard-32 are still available, but we recommend e2-standard-16 and e2-highmem-16 for cost efficiency. |
`enable_access_logging` |
`bool`
Optional. If true, private endpoint's access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each MatchRequest. Note that logs may incur a cost, especially if the deployed index receives a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`enable_datapoint_upsert_logging` |
`bool`
Optional. If true, logs to Cloud Logging errors relating to datapoint upserts. Under normal operation conditions, these log entries should be very rare. However, if incompatible datapoint updates are being uploaded to an index, a high volume of log entries may be generated in a short period of time. Note that logs may incur a cost, especially if the deployed index receives a high volume of datapoint upserts. Estimate your costs before enabling this option. |
`deployed_index_auth_config` |
Optional. If set, the authentication is enabled for the private endpoint. |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of reserved ip ranges under the VPC network that can be used for this DeployedIndex. If set, we will deploy the index within the provided ip ranges. Otherwise, the index might be deployed to any ip ranges under the provided VPC network. The value should be the name of the address (https://cloud.google.com/compute/docs/reference/rest/v1/addresses) Example: ['vertex-ai-ip-range']. For more information about subnets and network IP ranges, please see https://cloud.google.com/vpc/docs/subnets#manually_created_subnet_ip_ranges. |
`deployment_group` |
`str`
Optional. The deployment group can be no longer than 64 characters (eg: 'test', 'prod'). If not set, we will use the 'default' deployment group. Creating `deployment_groups` with `reserved_ip_ranges`
is a recommended practice when the peered network has
multiple peering ranges. This creates your deployments from
predictable IP spaces for easier traffic administration.
Also, one deployment_group (except 'default') can only be
used with the same reserved_ip_ranges which means if the
deployment_group has been used with reserved_ip_ranges: [a,
b, c], using it with [a, b] or [d, e] is disallowed.
Note: we only support up to 5 deployment groups(not
including 'default').
|
`deployment_tier` |
Optional. The deployment tier that the index is deployed to. DEPLOYMENT_TIER_UNSPECIFIED will use a system-chosen default tier. |
`psc_automation_configs` |
`MutableSequence[`
Optional. If set for PSC deployed index, PSC connection will be automatically created after deployment is done and the endpoint information is populated in private_endpoints.psc_automated_endpoints. |

## Classes

### DeploymentTier

`DeploymentTier(value)`


Tiers encapsulate serving time attributes like latency and throughput.

## Methods

### DeployedIndex

`DeployedIndex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient -->

# Class LlmUtilityServiceClient (1.134.0)

```
LlmUtilityServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for LLM related utility functions.

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
`LlmUtilityServiceTransport` |
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

### LlmUtilityServiceClient

```
LlmUtilityServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the llm utility service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,LlmUtilityServiceTransport,Callable[..., LlmUtilityServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the LlmUtilityServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### compute_tokens

```
compute_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.llm_utility_service.ComputeTokensRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.llm_utility_service.ComputeTokensResponse
```


Return a list of tokens based on the input text.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_compute_tokens():
# Create a client
client = aiplatform_v1beta1.
```[LlmUtilityServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ComputeTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[compute_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient.html#google_cloud_aiplatform_v1beta1_services_llm_utility_service_LlmUtilityServiceClient_compute_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ComputeTokens RPC call. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to get lists of tokens and token ids. This corresponds to the |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token computing API call. Schema is identical to the prediction schema of the text model, even for the non-text models, like chat models, or Codey models. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ComputeTokens RPC call. |

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
`LlmUtilityServiceClient` |
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
`LlmUtilityServiceClient` |
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
`LlmUtilityServiceClient` |
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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionCheckpointsAsyncPager -->

# Class ListModelVersionCheckpointsAsyncPager (1.134.0)

```
ListModelVersionCheckpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
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


A pager for iterating through `list_model_version_checkpoints`

requests.

This class thinly wraps an initial
[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`checkpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersionCheckpoints`

requests and continue to iterate
through the `checkpoints`

field on the
corresponding responses.

All the usual [ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionCheckpointsAsyncPager

```
ListModelVersionCheckpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuSpec -->

# Class BleuSpec (1.134.0)

`BleuSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

## Attribute |
|
|---|---|
Name |
Description |
`use_effective_order` |
`bool`
Optional. Whether to use_effective_order to compute bleu score. |

## Methods

### BleuSpec

`BleuSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardRunRequest -->

# Class DeleteTensorboardRunRequest (1.134.0)

`DeleteTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboardRun.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardRun to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### DeleteTensorboardRunRequest

`DeleteTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboardRun.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessInstance -->

# Class QuestionAnsweringCorrectnessInstance (1.134.0)

```
QuestionAnsweringCorrectnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness instance.

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
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringCorrectnessInstance

```
QuestionAnsweringCorrectnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectorySingleToolUseInput -->

# Class TrajectorySingleToolUseInput (1.134.0)

```
TrajectorySingleToolUseInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instances and metric spec for TrajectorySingleToolUse metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for TrajectorySingleToolUse metric. |
`instances` |
`MutableSequence[`
Required. Repeated TrajectorySingleToolUse instance. |

## Methods

### TrajectorySingleToolUseInput

```
TrajectorySingleToolUseInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instances and metric spec for TrajectorySingleToolUse metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RestoreDatasetVersionRequest -->

# Class RestoreDatasetVersionRequest (1.134.0)

```
RestoreDatasetVersionRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DatasetService.RestoreDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DatasetVersion resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|

## Methods

### RestoreDatasetVersionRequest

```
RestoreDatasetVersionRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DatasetService.RestoreDatasetVersion.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ColabImage -->

# Class ColabImage (1.134.0)

`ColabImage(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Colab image of the runtime.

## Attributes |
|
|---|---|
Name |
Description |
`release_name` |
`str`
Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release. |
`description` |
`str`
Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11". |

## Methods

### ColabImage

`ColabImage(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Colab image of the runtime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchInput -->

# Class TrajectoryAnyOrderMatchInput (1.134.0)

```
TrajectoryAnyOrderMatchInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instances and metric spec for TrajectoryAnyOrderMatch metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for TrajectoryAnyOrderMatch metric. |
`instances` |
`MutableSequence[`
Required. Repeated TrajectoryAnyOrderMatch instance. |

## Methods

### TrajectoryAnyOrderMatchInput

```
TrajectoryAnyOrderMatchInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instances and metric spec for TrajectoryAnyOrderMatch metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager -->

# Class ListPersistentResourcesAsyncPager (1.134.0)

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
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


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPersistentResourcesAsyncPager

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardExperimentsAsyncPager -->

# Class ListTensorboardExperimentsAsyncPager (1.134.0)

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsAsyncPager

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceSpec -->

# Class QuestionAnsweringRelevanceSpec (1.134.0)

```
QuestionAnsweringRelevanceSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering relevance. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringRelevanceSpec

```
QuestionAnsweringRelevanceSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsRequest -->

# Class RemoveDatapointsRequest (1.134.0)

`RemoveDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.RemoveDatapoints

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`str`
Required. The name of the Index resource to be updated. Format: `projects/{project}/locations/{location}/indexes/{index}`
|
`datapoint_ids` |
`MutableSequence[str]`
A list of datapoint ids to be deleted. |

## Methods

### RemoveDatapointsRequest

`RemoveDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.RemoveDatapoints

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureViewRequest -->

# Class UpdateFeatureViewRequest (1.134.0)

`UpdateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.UpdateFeatureView.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
Required. The FeatureView's `name` field is used to
identify the FeatureView to be updated. Format:
`projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureView resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `service_agent_type`
- `big_query_source`
- `big_query_source.uri`
- `big_query_source.entity_id_columns`
- `feature_registry_source`
- `feature_registry_source.feature_groups`
- `sync_config`
- `sync_config.cron`
- `optimized_config.automatic_resources`
|

## Methods

### UpdateFeatureViewRequest

`UpdateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.UpdateFeatureView.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager -->

# Class ListFeatureOnlineStoresPager (1.134.0)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureOnlineStoresPager

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager -->

# Class QueryDeployedModelsAsyncPager (1.134.0)

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsAsyncPager

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringAlertsPager -->

# Class SearchModelMonitoringAlertsPager (1.134.0)

```
SearchModelMonitoringAlertsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse,
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


A pager for iterating through `search_model_monitoring_alerts`

requests.

This class thinly wraps an initial
[SearchModelMonitoringAlertsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_monitoring_alerts`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelMonitoringAlerts`

requests and continue to iterate
through the `model_monitoring_alerts`

field on the
corresponding responses.

All the usual [SearchModelMonitoringAlertsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelMonitoringAlertsPager

```
SearchModelMonitoringAlertsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.StudyStoppingConfig -->

# Class StudyStoppingConfig (1.134.0)

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

## Attributes |
|
|---|---|
Name |
Description |
`should_stop_asap` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, a Study enters STOPPING_ASAP whenever it would normally enters STOPPING state. The bottom line is: set to true if you want to interrupt on-going evaluations of Trials as soon as the study stopping condition is met. (Please see Study.State documentation for the source of truth). |
`minimum_runtime_constraint` |
Each "stopping rule" in this proto specifies an "if" condition. Before Vizier would generate a new suggestion, it first checks each specified stopping rule, from top to bottom in this list. Note that the first few rules (e.g. minimum_runtime_constraint, min_num_trials) will prevent other stopping rules from being evaluated until they are met. For example, setting `min_num_trials=5` and
`always_stop_after= 1 hour` means that the Study will ONLY
stop after it has 5 COMPLETED trials, even if more than an
hour has passed since its creation. It follows the first
applicable rule (whose "if" condition is satisfied) to make
a stopping decision. If none of the specified rules are
applicable, then Vizier decides that the study should not
stop. If Vizier decides that the study should stop, the
study enters STOPPING state (or STOPPING_ASAP if
should_stop_asap = true). IMPORTANT: The automatic study
state transition happens precisely as described above; that
is, deleting trials or updating StudyConfig NEVER
automatically moves the study state back to ACTIVE. If you
want to *resume* a Study that was stopped, 1) change the
stopping conditions if necessary, 2) activate the study, and
then 3) ask for suggestions. If the specified time or
duration has not passed, do not stop the study.
|
`maximum_runtime_constraint` |
If the specified time or duration has passed, stop the study. |
`min_num_trials` |
`google.protobuf.wrappers_pb2.Int32Value`
If there are fewer than this many COMPLETED trials, do not stop the study. |
`max_num_trials` |
`google.protobuf.wrappers_pb2.Int32Value`
If there are more than this many trials, stop the study. |
`max_num_trials_no_progress` |
`google.protobuf.wrappers_pb2.Int32Value`
If the objective value has not improved for this many consecutive trials, stop the study. WARNING: Effective only for single-objective studies. |
`max_duration_no_progress` |
`google.protobuf.duration_pb2.Duration`
If the objective value has not improved for this much time, stop the study. WARNING: Effective only for single-objective studies. |

## Methods

### StudyStoppingConfig

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDataLabelingJobRequest -->

# Class CreateDataLabelingJobRequest (1.134.0)

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`data_labeling_job` |
Required. The DataLabelingJob to create. |

## Methods

### CreateDataLabelingJobRequest

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensResponse -->

# Class ComputeTokensResponse (1.134.0)

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.

## Attribute |
|
|---|---|
Name |
Description |
`tokens_info` |
`MutableSequence[`
Lists of tokens info from the input. A ComputeTokensRequest could have multiple instances with a prompt in each instance. We also need to return lists of tokens info for the request with multiple instances. |

## Methods

### ComputeTokensResponse

`ComputeTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ComputeTokens RPC call.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse -->

# Class ListSpecialistPoolsResponse (1.134.0)

`ListSpecialistPoolsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SpecialistPoolService.ListSpecialistPools.

## Attributes |
|
|---|---|
Name |
Description |
`specialist_pools` |
`MutableSequence[`
A list of SpecialistPools that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListSpecialistPoolsResponse

`ListSpecialistPoolsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SpecialistPoolService.ListSpecialistPools.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelTrainingPipelineRequest -->

# Class CancelTrainingPipelineRequest (1.134.0)

```
CancelTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CancelTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline to cancel. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### CancelTrainingPipelineRequest

```
CancelTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CancelTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsAsyncPager -->

# Class ListFeatureMonitorJobsAsyncPager (1.134.0)

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

## Methods

### ListFeatureMonitorJobsAsyncPager

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessInstance -->

# Class QuestionAnsweringCorrectnessInstance (1.134.0)

```
QuestionAnsweringCorrectnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness instance.

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
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringCorrectnessInstance

```
QuestionAnsweringCorrectnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelArmorConfig -->

# Class ModelArmorConfig (1.134.0)

`ModelArmorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Model Armor integrations of prompt and responses.

## Attributes |
|
|---|---|
Name |
Description |
`prompt_template_name` |
`str`
Optional. The name of the Model Armor template to use for prompt sanitization. |
`response_template_name` |
`str`
Optional. The name of the Model Armor template to use for response sanitization. |

## Methods

### ModelArmorConfig

`ModelArmorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Model Armor integrations of prompt and responses.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest.FeatureSpec -->

# Class FeatureSpec (1.134.0)

`FeatureSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines the Feature value(s) to import.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Required. ID of the Feature to import values of. This Feature must exist in the target EntityType, or the request will fail. |
`source_field` |
`str`
Source column to get the Feature values from. If not set, uses the column with the same name as the Feature ID. |

## Methods

### FeatureSpec

`FeatureSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines the Feature value(s) to import.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager -->

# Class ListNotebookExecutionJobsAsyncPager (1.134.0)

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookExecutionJobsAsyncPager

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager -->

# Class SearchMigratableResourcesAsyncPager (1.134.0)

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchMigratableResourcesAsyncPager

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessInstance -->

# Class QuestionAnsweringHelpfulnessInstance (1.134.0)

```
QuestionAnsweringHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness instance.

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
`context` |
`str`
Optional. Text provided as context to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. The question asked and other instruction in the inference prompt. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### QuestionAnsweringHelpfulnessInstance

```
QuestionAnsweringHelpfulnessInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationDataset -->

# Class EvaluationDataset (1.134.0)

`EvaluationDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dataset used for evaluation.

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
Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported. This field is a member of `oneof` _ `source` .
|
`bigquery_source` |
BigQuery source holds the dataset. This field is a member of `oneof` _ `source` .
|

## Methods

### EvaluationDataset

`EvaluationDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dataset used for evaluation.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.StudyStoppingConfig -->

# Class StudyStoppingConfig (1.134.0)

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

## Attributes |
|
|---|---|
Name |
Description |
`should_stop_asap` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, a Study enters STOPPING_ASAP whenever it would normally enters STOPPING state. The bottom line is: set to true if you want to interrupt on-going evaluations of Trials as soon as the study stopping condition is met. (Please see Study.State documentation for the source of truth). |
`minimum_runtime_constraint` |
Each "stopping rule" in this proto specifies an "if" condition. Before Vizier would generate a new suggestion, it first checks each specified stopping rule, from top to bottom in this list. Note that the first few rules (e.g. minimum_runtime_constraint, min_num_trials) will prevent other stopping rules from being evaluated until they are met. For example, setting `min_num_trials=5` and
`always_stop_after= 1 hour` means that the Study will ONLY
stop after it has 5 COMPLETED trials, even if more than an
hour has passed since its creation. It follows the first
applicable rule (whose "if" condition is satisfied) to make
a stopping decision. If none of the specified rules are
applicable, then Vizier decides that the study should not
stop. If Vizier decides that the study should stop, the
study enters STOPPING state (or STOPPING_ASAP if
should_stop_asap = true). IMPORTANT: The automatic study
state transition happens precisely as described above; that
is, deleting trials or updating StudyConfig NEVER
automatically moves the study state back to ACTIVE. If you
want to *resume* a Study that was stopped, 1) change the
stopping conditions if necessary, 2) activate the study, and
then 3) ask for suggestions. If the specified time or
duration has not passed, do not stop the study.
|
`maximum_runtime_constraint` |
If the specified time or duration has passed, stop the study. |
`min_num_trials` |
`google.protobuf.wrappers_pb2.Int32Value`
If there are fewer than this many COMPLETED trials, do not stop the study. |
`max_num_trials` |
`google.protobuf.wrappers_pb2.Int32Value`
If there are more than this many trials, stop the study. |
`max_num_trials_no_progress` |
`google.protobuf.wrappers_pb2.Int32Value`
If the objective value has not improved for this many consecutive trials, stop the study. WARNING: Effective only for single-objective studies. |
`max_duration_no_progress` |
`google.protobuf.duration_pb2.Duration`
If the objective value has not improved for this much time, stop the study. WARNING: Effective only for single-objective studies. |

## Methods

### StudyStoppingConfig

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel -->

# Class PublisherModel (1.134.0)

`PublisherModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Model Garden Publisher Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the PublisherModel. |
`version_id` |
`str`
Output only. Immutable. The version ID of the PublisherModel. A new version is committed when a new model version is uploaded under an existing model id. It is an auto-incrementing decimal number in string representation. |
`open_source_category` |
Required. Indicates the open source category of the publisher model. |
`parent` |
Optional. The parent that this model was customized from. E.g., Vision API, Natural Language API, LaMDA, T5, etc. Foundation models don't have parents. |
`supported_actions` |
Optional. Supported call-to-action options. |
`frameworks` |
`MutableSequence[str]`
Optional. Additional information about the model's Frameworks. |
`launch_stage` |
Optional. Indicates the launch stage of the model. |
`version_state` |
Optional. Indicates the state of the model version. |
`publisher_model_template` |
`str`
Optional. Output only. Immutable. Used to indicate this model has a publisher model and provide the template of the publisher model resource name. |
`predict_schemata` |
Optional. The schemata that describes formats of the PublisherModel's predictions and explanations as given and returned via PredictionService.Predict. |

## Classes

### CallToAction

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Documentation

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

### OpenSourceCategory

`OpenSourceCategory(value)`


An enum representing the open source category of a PublisherModel.

### Parent

`Parent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The information about the parent of a model.

### ResourceReference

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### VersionState

`VersionState(value)`


An enum representing the state of the PublicModelVersion.

## Methods

### PublisherModel

`PublisherModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Model Garden Publisher Model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SyncFeatureViewResponse -->

# Class SyncFeatureViewResponse (1.134.0)

`SyncFeatureViewResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.SyncFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`feature_view_sync` |
`str`
Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### SyncFeatureViewResponse

`SyncFeatureViewResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.SyncFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IdMatcher -->

# Class IdMatcher (1.134.0)

`IdMatcher(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Matcher for Features of an EntityType by Feature ID.

## Attribute |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[str]`
Required. The following are accepted as `ids` :
- A single-element list containing only `*` , which selects
all Features in the target EntityType, or
- A list containing only Feature IDs, which selects only
Features with those IDs in the target EntityType.
|

## Methods

### IdMatcher

`IdMatcher(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Matcher for Features of an EntityType by Feature ID.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse -->

# Class ListNasJobsResponse (1.134.0)

`ListNasJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasJobs

## Attributes |
|
|---|---|
Name |
Description |
`nas_jobs` |
`MutableSequence[`
List of NasJobs in the requested page. NasJob.nas_job_output of the jobs will not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListNasJobsRequest.page_token to obtain that page. |

## Methods

### ListNasJobsResponse

`ListNasJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasJobs

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolOperationMetadata -->

# Class UpdateDeploymentResourcePoolOperationMetadata (1.134.0)

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateDeploymentResourcePoolOperationMetadata

```
UpdateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for UpdateDeploymentResourcePool method.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportEvaluatedAnnotationsResponse -->

# Class BatchImportEvaluatedAnnotationsResponse (1.134.0)

```
BatchImportEvaluatedAnnotationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportEvaluatedAnnotations

## Attribute |
|
|---|---|
Name |
Description |
`imported_evaluated_annotations_count` |
`int`
Output only. Number of EvaluatedAnnotations imported. |

## Methods

### BatchImportEvaluatedAnnotationsResponse

```
BatchImportEvaluatedAnnotationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportEvaluatedAnnotations

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDeploymentResourcePoolOperationMetadata -->

# Class CreateDeploymentResourcePoolOperationMetadata (1.134.0)

```
CreateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for CreateDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDeploymentResourcePoolOperationMetadata

```
CreateDeploymentResourcePoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for CreateDeploymentResourcePool method.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse -->

# Class ListRagCorporaResponse (1.134.0)

`ListRagCorporaResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagCorpora.

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpora` |
`MutableSequence[`
List of RagCorpora in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListRagCorporaRequest.page_token to obtain that page. |

## Methods

### ListRagCorporaResponse

`ListRagCorporaResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagCorpora.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetySetting.HarmBlockThreshold -->

# Class HarmBlockThreshold (1.134.0)

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

## Enums |
|
|---|---|
Name |
Description |
`HARM_BLOCK_THRESHOLD_UNSPECIFIED` |
Unspecified harm block threshold. |
`BLOCK_LOW_AND_ABOVE` |
Block low threshold and above (i.e. block more). |
`BLOCK_MEDIUM_AND_ABOVE` |
Block medium threshold and above. |
`BLOCK_ONLY_HIGH` |
Block only high threshold (i.e. block less). |
`BLOCK_NONE` |
Block none. |
`OFF` |
Turn off the safety filter. |

## Methods

### HarmBlockThreshold

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDirectWriteResponse.WriteResponse -->

# Class WriteResponse (1.134.0)

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

## Attributes |
|
|---|---|
Name |
Description |
`data_key` |
What key is this write response associated with. |
`online_store_write_time` |
`google.protobuf.timestamp_pb2.Timestamp`
When the feature values were written to the online store. If FeatureViewDirectWriteResponse.status is not OK, this field is not populated. |

## Methods

### WriteResponse

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookRuntimeTemplateOperationMetadata -->

# Class CreateNotebookRuntimeTemplateOperationMetadata (1.134.0)

```
CreateNotebookRuntimeTemplateOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookRuntimeTemplate.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateNotebookRuntimeTemplateOperationMetadata

```
CreateNotebookRuntimeTemplateOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookRuntimeTemplate.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardRunRequest -->

# Class DeleteTensorboardRunRequest (1.134.0)

`DeleteTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboardRun.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardRun to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### DeleteTensorboardRunRequest

`DeleteTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.DeleteTensorboardRun.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionRequest -->

# Class RestoreDatasetVersionRequest (1.134.0)

```
RestoreDatasetVersionRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DatasetService.RestoreDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DatasetVersion resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|

## Methods

### RestoreDatasetVersionRequest

```
RestoreDatasetVersionRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DatasetService.RestoreDatasetVersion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager -->

# Class ListDeploymentResourcePoolsPager (1.134.0)

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDeploymentResourcePools`

requests and continue to iterate
through the `deployment_resource_pools`

field on the
corresponding responses.

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDeploymentResourcePoolsPager

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TuningDataStats -->

# Class TuningDataStats (1.134.0)

`TuningDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The tuning data statistic values for TuningJob.

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
`supervised_tuning_data_stats` |
The SFT Tuning data stats. This field is a member of `oneof` _ `tuning_data_stats` .
|
`distillation_data_stats` |
Output only. Statistics for distillation. This field is a member of `oneof` _ `tuning_data_stats` .
|

## Methods

### TuningDataStats

`TuningDataStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The tuning data statistic values for TuningJob.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ColabImage -->

# Class ColabImage (1.134.0)

`ColabImage(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Colab image of the runtime.

## Attributes |
|
|---|---|
Name |
Description |
`release_name` |
`str`
Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release. |
`description` |
`str`
Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11". |

## Methods

### ColabImage

`ColabImage(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Colab image of the runtime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SecretEnvVar -->

# Class SecretEnvVar (1.134.0)

`SecretEnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable where the value is a secret in Cloud Secret Manager.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name of the secret environment variable. |
`secret_ref` |
Required. Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable. |

## Methods

### SecretEnvVar

`SecretEnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable where the value is a secret in Cloud Secret Manager.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager -->

# Class ListNotebookRuntimeTemplatesAsyncPager (1.134.0)

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimeTemplatesAsyncPager

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardTimeSeriesResponse -->

# Class BatchCreateTensorboardTimeSeriesResponse (1.134.0)

```
BatchCreateTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The created TensorboardTimeSeries. |

## Methods

### BatchCreateTensorboardTimeSeriesResponse

```
BatchCreateTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenAiAdvancedFeaturesConfig -->

# Class GenAiAdvancedFeaturesConfig (1.134.0)

`GenAiAdvancedFeaturesConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for GenAiAdvancedFeatures.

## Attribute |
|
|---|---|
Name |
Description |
`rag_config` |
Configuration for Retrieval Augmented Generation feature. |

## Classes

### RagConfig

`RagConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Retrieval Augmented Generation feature.

## Methods

### GenAiAdvancedFeaturesConfig

`GenAiAdvancedFeaturesConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for GenAiAdvancedFeatures.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VoiceConfig -->

# Class VoiceConfig (1.134.0)

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

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
`prebuilt_voice_config` |
The configuration for a prebuilt voice. This field is a member of `oneof` _ `voice_config` .
|
`replicated_voice_config` |
Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. This field is a member of `oneof` _ `voice_config` .
|

## Methods

### VoiceConfig

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.CallToAction.Deploy -->

# Class Deploy (1.134.0)

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

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
`model_display_name` |
`str`
Optional. Default model display name. |
`large_model_reference` |
Optional. Large model reference. When this is set, model_artifact_spec is not needed. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying this Model in Vertex AI. Not present for Large Models. |
`artifact_uri` |
`str`
Optional. The path to the directory containing the Model artifact and any of its supporting files. |
`deploy_task_name` |
`str`
Optional. The name of the deploy task (e.g., "text to image generation"). This field is a member of `oneof` _ `_deploy_task_name` .
|
`deploy_metadata` |
Optional. Metadata information about this deployment config. This field is a member of `oneof` _ `_deploy_metadata` .
|
`title` |
`str`
Required. The title of the regional resource reference. |
`public_artifact_uri` |
`str`
Optional. The signed URI for ephemeral Cloud Storage access to model artifact. |

## Classes

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Methods

### Deploy

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDataLabelingJobRequest -->

# Class CreateDataLabelingJobRequest (1.134.0)

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the DataLabelingJob. Format: `projects/{project}/locations/{location}`
|
`data_labeling_job` |
Required. The DataLabelingJob to create. |

## Methods

### CreateDataLabelingJobRequest

```
CreateDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateDataLabelingJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse -->

# Class ListDataLabelingJobsResponse (1.134.0)

```
ListDataLabelingJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`data_labeling_jobs` |
`MutableSequence[`
A list of DataLabelingJobs that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListDataLabelingJobsResponse

```
ListDataLabelingJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListDataLabelingJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse -->

# Class ListPipelineJobsResponse (1.134.0)

`ListPipelineJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PipelineService.ListPipelineJobs

## Attributes |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
List of PipelineJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListPipelineJobsRequest.page_token to obtain that page. |

## Methods

### ListPipelineJobsResponse

`ListPipelineJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PipelineService.ListPipelineJobs

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelArmorConfig -->

# Class ModelArmorConfig (1.134.0)

`ModelArmorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Model Armor integrations of prompt and responses.

## Attributes |
|
|---|---|
Name |
Description |
`prompt_template_name` |
`str`
Optional. The name of the Model Armor template to use for prompt sanitization. |
`response_template_name` |
`str`
Optional. The name of the Model Armor template to use for response sanitization. |

## Methods

### ModelArmorConfig

`ModelArmorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Model Armor integrations of prompt and responses.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitoringJobsAsyncPager -->

# Class ListModelMonitoringJobsAsyncPager (1.134.0)

```
ListModelMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
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


A pager for iterating through `list_model_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_monitoring_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelMonitoringJobs`

requests and continue to iterate
through the `model_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitoringJobsAsyncPager

```
ListModelMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.BatchPredictionValidationAssessmentConfig -->

# Class BatchPredictionValidationAssessmentConfig (1.134.0)

```
BatchPredictionValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction validation assessment.

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. The name of the model used for batch prediction. |

## Methods

### BatchPredictionValidationAssessmentConfig

```
BatchPredictionValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction validation assessment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse -->

# Class ListSpecialistPoolsResponse (1.134.0)

`ListSpecialistPoolsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SpecialistPoolService.ListSpecialistPools.

## Attributes |
|
|---|---|
Name |
Description |
`specialist_pools` |
`MutableSequence[`
A list of SpecialistPools that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListSpecialistPoolsResponse

`ListSpecialistPoolsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SpecialistPoolService.ListSpecialistPools.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequestResponseLoggingConfig -->

# Class PredictRequestResponseLoggingConfig (1.134.0)

```
PredictRequestResponseLoggingConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for logging request-response to a BigQuery table.

## Attributes |
|
|---|---|
Name |
Description |
`enabled` |
`bool`
If logging is enabled or not. |
`sampling_rate` |
`float`
Percentage of requests to be logged, expressed as a fraction in range(0,1]. |
`bigquery_destination` |
BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_` where will
be made BigQuery-dataset-name compatible (e.g. most special
characters will become underscores). If no table name is
given, a new table will be created with name
`request_response_logging`
|
`request_response_logging_schema_version` |
`str`
Output only. The schema version used in creating the BigQuery table for the request response logging. The versions are "v1" and "v2". The current default version is "v1". |
`enable_otel_logging` |
`bool`
This field is used for large models. If true, in addition to the original large model logs, logs will be converted in OTel schema format, and saved in otel_log column. Default value is false. |

## Methods

### PredictRequestResponseLoggingConfig

```
PredictRequestResponseLoggingConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for logging request-response to a BigQuery table.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy -->

# Class Deploy (1.134.0)

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

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
`model_display_name` |
`str`
Optional. Default model display name. |
`large_model_reference` |
Optional. Large model reference. When this is set, model_artifact_spec is not needed. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying this Model in Vertex AI. Not present for Large Models. |
`artifact_uri` |
`str`
Optional. The path to the directory containing the Model artifact and any of its supporting files. |
`deploy_task_name` |
`str`
Optional. The name of the deploy task (e.g., "text to image generation"). This field is a member of `oneof` _ `_deploy_task_name` .
|
`deploy_metadata` |
Optional. Metadata information about this deployment config. This field is a member of `oneof` _ `_deploy_metadata` .
|
`title` |
`str`
Required. The title of the regional resource reference. |
`public_artifact_uri` |
`str`
Optional. The signed URI for ephemeral Cloud Storage access to model artifact. |

## Classes

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Methods

### Deploy

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesAsyncPager -->

# Class ListTensorboardTimeSeriesAsyncPager (1.134.0)

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardTimeSeriesAsyncPager

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager -->

# Class ListHyperparameterTuningJobsAsyncPager (1.134.0)

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

## Methods

### ListHyperparameterTuningJobsAsyncPager

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadTensorboardTimeSeriesDataResponse -->

# Class BatchReadTensorboardTimeSeriesDataResponse (1.134.0)

```
BatchReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchReadTensorboardTimeSeriesData.

## Attribute |
|
|---|---|
Name |
Description |
`time_series_data` |
`MutableSequence[`
The returned time series data. |

## Methods

### BatchReadTensorboardTimeSeriesDataResponse

```
BatchReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchReadTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse -->

# Class ListNasJobsResponse (1.134.0)

`ListNasJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasJobs

## Attributes |
|
|---|---|
Name |
Description |
`nas_jobs` |
`MutableSequence[`
List of NasJobs in the requested page. NasJob.nas_job_output of the jobs will not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListNasJobsRequest.page_token to obtain that page. |

## Methods

### ListNasJobsResponse

`ListNasJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasJobs

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse -->

# Class ListExtensionsResponse (1.134.0)

`ListExtensionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionRegistryService.ListExtensions

## Attributes |
|
|---|---|
Name |
Description |
`extensions` |
`MutableSequence[`
List of Extension in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListExtensionsRequest.page_token to obtain that page. |

## Methods

### ListExtensionsResponse

`ListExtensionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionRegistryService.ListExtensions

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsResponse -->

# Class BatchImportEvaluatedAnnotationsResponse (1.134.0)

```
BatchImportEvaluatedAnnotationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportEvaluatedAnnotations

## Attribute |
|
|---|---|
Name |
Description |
`imported_evaluated_annotations_count` |
`int`
Output only. Number of EvaluatedAnnotations imported. |

## Methods

### BatchImportEvaluatedAnnotationsResponse

```
BatchImportEvaluatedAnnotationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportEvaluatedAnnotations

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelBatchPredictionJobRequest -->

# Class CancelBatchPredictionJobRequest (1.134.0)

```
CancelBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob to cancel. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### CancelBatchPredictionJobRequest

```
CancelBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelBatchPredictionJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateRequest -->

# Class CheckTrialEarlyStoppingStateRequest (1.134.0)

```
CheckTrialEarlyStoppingStateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VizierService.CheckTrialEarlyStoppingState.

## Attribute |
|
|---|---|
Name |
Description |
`trial_name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### CheckTrialEarlyStoppingStateRequest

```
CheckTrialEarlyStoppingStateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VizierService.CheckTrialEarlyStoppingState.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VoiceConfig -->

# Class VoiceConfig (1.134.0)

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

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
`prebuilt_voice_config` |
The configuration for a prebuilt voice. This field is a member of `oneof` _ `voice_config` .
|
`replicated_voice_config` |
Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. This field is a member of `oneof` _ `voice_config` .
|

## Methods

### VoiceConfig

`VoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a voice.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service -->

# Package feature_online_store_service (1.134.0)

API documentation for `aiplatform_v1.services.feature_online_store_service`

package.

## Classes

[FeatureOnlineStoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient)

A service for fetching feature values from the online store.

[FeatureOnlineStoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient)

A service for fetching feature values from the online store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureViewRequest -->

# Class DeleteFeatureViewRequest (1.134.0)

`DeleteFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.DeleteFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureView to be deleted. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### DeleteFeatureViewRequest

`DeleteFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.DeleteFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FractionSplit -->

# Class FractionSplit (1.134.0)

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### FractionSplit

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager -->

# Class ListModelDeploymentMonitoringJobsPager (1.134.0)

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

## Methods

### ListModelDeploymentMonitoringJobsPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetySetting.HarmBlockThreshold -->

# Class HarmBlockThreshold (1.134.0)

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

## Enums |
|
|---|---|
Name |
Description |
`HARM_BLOCK_THRESHOLD_UNSPECIFIED` |
Unspecified harm block threshold. |
`BLOCK_LOW_AND_ABOVE` |
Block low threshold and above (i.e. block more). |
`BLOCK_MEDIUM_AND_ABOVE` |
Block medium threshold and above. |
`BLOCK_ONLY_HIGH` |
Block only high threshold (i.e. block less). |
`BLOCK_NONE` |
Block none. |
`OFF` |
Turn off the safety filter. |

## Methods

### HarmBlockThreshold

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesResponse -->

# Class SearchExamplesResponse (1.134.0)

`SearchExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.SearchExamples.

## Attribute |
|
|---|---|
Name |
Description |
`results` |
`MutableSequence[`
The results of searching for similar examples. |

## Classes

### SimilarExample

`SimilarExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result of the similar example.

## Methods

### SearchExamplesResponse

`SearchExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.SearchExamples.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictResponse -->

# Class PredictResponse (1.134.0)

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.

## Attributes |
|
|---|---|
Name |
Description |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. The schema of any single prediction may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] prediction_schema_uri. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this prediction. |
`model` |
`str`
Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_version_id` |
`str`
Output only. The version ID of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_display_name` |
`str`
Output only. The [display name][google.cloud.aiplatform.v1.Model.display_name] of the Model which is deployed as the DeployedModel that this prediction hits. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation. |

## Methods

### PredictResponse

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataPager -->

# Class ExportTensorboardTimeSeriesDataPager (1.134.0)

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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


A pager for iterating through `export_tensorboard_time_series_data`

requests.

This class thinly wraps an initial
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse) object, and
provides an `__iter__`

method to iterate through its
`time_series_data_points`

field.

If there are more pages, the `__iter__`

method will make additional
`ExportTensorboardTimeSeriesData`

requests and continue to iterate
through the `time_series_data_points`

field on the
corresponding responses.

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ExportTensorboardTimeSeriesDataPager

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardTimeSeriesResponse -->

# Class BatchCreateTensorboardTimeSeriesResponse (1.134.0)

```
BatchCreateTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The created TensorboardTimeSeries. |

## Methods

### BatchCreateTensorboardTimeSeriesResponse

```
BatchCreateTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchCreateTensorboardTimeSeries.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenAiAdvancedFeaturesConfig -->

# Class GenAiAdvancedFeaturesConfig (1.134.0)

`GenAiAdvancedFeaturesConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for GenAiAdvancedFeatures.

## Attribute |
|
|---|---|
Name |
Description |
`rag_config` |
Configuration for Retrieval Augmented Generation feature. |

## Classes

### RagConfig

`RagConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Retrieval Augmented Generation feature.

## Methods

### GenAiAdvancedFeaturesConfig

`GenAiAdvancedFeaturesConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for GenAiAdvancedFeatures.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTrainingPipelineRequest -->

# Class DeleteTrainingPipelineRequest (1.134.0)

```
DeleteTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.DeleteTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### DeleteTrainingPipelineRequest

```
DeleteTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.DeleteTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SecretEnvVar -->

# Class SecretEnvVar (1.134.0)

`SecretEnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable where the value is a secret in Cloud Secret Manager.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Name of the secret environment variable. |
`secret_ref` |
Required. Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable. |

## Methods

### SecretEnvVar

`SecretEnvVar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents an environment variable where the value is a secret in Cloud Secret Manager.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexRequest -->

# Class UpdateIndexRequest (1.134.0)

`UpdateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
Required. The Index which updates the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexRequest

`UpdateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpdateIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteResponse.WriteResponse -->

# Class WriteResponse (1.134.0)

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

## Attributes |
|
|---|---|
Name |
Description |
`data_key` |
What key is this write response associated with. |
`online_store_write_time` |
`google.protobuf.timestamp_pb2.Timestamp`
When the feature values were written to the online store. If FeatureViewDirectWriteResponse.status is not OK, this field is not populated. |

## Methods

### WriteResponse

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateOperationMetadata -->

# Class CreateNotebookRuntimeTemplateOperationMetadata (1.134.0)

```
CreateNotebookRuntimeTemplateOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookRuntimeTemplate.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateNotebookRuntimeTemplateOperationMetadata

```
CreateNotebookRuntimeTemplateOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.CreateNotebookRuntimeTemplate.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe.TcpSocketAction -->

# Class TcpSocketAction (1.134.0)

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Number of the port to access on the container. Number must be in the range 1 to 65535. |
`host` |
`str`
Optional: Host name to connect to, defaults to the model serving container's IP. |

## Methods

### TcpSocketAction

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsAsyncPager -->

# Class ListFeatureViewSyncsAsyncPager (1.134.0)

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewSyncsAsyncPager

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FractionSplit -->

# Class FractionSplit (1.134.0)

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### FractionSplit

`FractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesResponse -->

# Class GenerateMemoriesResponse (1.134.0)

`GenerateMemoriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MemoryBankService.GenerateMemories.

## Attribute |
|
|---|---|
Name |
Description |
`generated_memories` |
`MutableSequence[`
The generated memories. |

## Classes

### GeneratedMemory

`GeneratedMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory generated by the operation.

## Methods

### GenerateMemoriesResponse

`GenerateMemoriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MemoryBankService.GenerateMemories.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse -->

# Class ListDataLabelingJobsResponse (1.134.0)

```
ListDataLabelingJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListDataLabelingJobs.

## Attributes |
|
|---|---|
Name |
Description |
`data_labeling_jobs` |
`MutableSequence[`
A list of DataLabelingJobs that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListDataLabelingJobsResponse

```
ListDataLabelingJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListDataLabelingJobs.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessSpec -->

# Class QuestionAnsweringCorrectnessSpec (1.134.0)

```
QuestionAnsweringCorrectnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering correctness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringCorrectnessSpec

```
QuestionAnsweringCorrectnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse -->

# Class ListPersistentResourcesResponse (1.134.0)

```
ListPersistentResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PersistentResourceService.ListPersistentResources

## Attribute |
|
|---|---|
Name |
Description |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListPersistentResourcesRequest.page_token to obtain that page. |

## Methods

### ListPersistentResourcesResponse

```
ListPersistentResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PersistentResourceService.ListPersistentResources

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringHelpfulnessSpec -->

# Class QuestionAnsweringHelpfulnessSpec (1.134.0)

```
QuestionAnsweringHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering helpfulness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringHelpfulnessSpec

```
QuestionAnsweringHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.State -->

# Class State (1.134.0)

`State(value)`


Possible state of the schedule.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified. |
`ACTIVE` |
The Schedule is active. Runs are being scheduled on the user-specified timespec. |
`PAUSED` |
The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete. |
`COMPLETED` |
The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

## Methods

### State

`State(value)`


Possible state of the schedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager -->

# Class ListPersistentResourcesAsyncPager (1.134.0)

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
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


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPersistentResourcesAsyncPager

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardExperimentsAsyncPager -->

# Class ListTensorboardExperimentsAsyncPager (1.134.0)

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsAsyncPager

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexOperationMetadata -->

# Class CreateIndexOperationMetadata (1.134.0)

```
CreateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.CreateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### CreateIndexOperationMetadata

```
CreateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.CreateIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexOperationMetadata -->

# Class UpdateIndexOperationMetadata (1.134.0)

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### UpdateIndexOperationMetadata

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse -->

# Class ListPipelineJobsResponse (1.134.0)

`ListPipelineJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PipelineService.ListPipelineJobs

## Attributes |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
List of PipelineJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListPipelineJobsRequest.page_token to obtain that page. |

## Methods

### ListPipelineJobsResponse

`ListPipelineJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PipelineService.ListPipelineJobs

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadTensorboardTimeSeriesDataResponse -->

# Class BatchReadTensorboardTimeSeriesDataResponse (1.134.0)

```
BatchReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchReadTensorboardTimeSeriesData.

## Attribute |
|
|---|---|
Name |
Description |
`time_series_data` |
`MutableSequence[`
The returned time series data. |

## Methods

### BatchReadTensorboardTimeSeriesDataResponse

```
BatchReadTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.BatchReadTensorboardTimeSeriesData.
