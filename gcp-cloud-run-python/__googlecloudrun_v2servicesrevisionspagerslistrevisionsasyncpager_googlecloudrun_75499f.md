---
merged_at: 2026-01-25T15:25:49.601594
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2servicesrevisionspagerslistrevisionsasyncpager_googlecloudrun__63c452.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesrevisionspagerslistrevisionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers.ListRevisionsAsyncPager -->

# Class ListRevisionsAsyncPager (0.14.0)

```
ListRevisionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.revision.ListRevisionsResponse],
],
request: google.cloud.run_v2.types.revision.ListRevisionsRequest,
response: google.cloud.run_v2.types.revision.ListRevisionsResponse,
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


A pager for iterating through `list_revisions`

requests.

This class thinly wraps an initial
[ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`revisions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRevisions`

requests and continue to iterate
through the `revisions`

field on the
corresponding responses.

All the usual [ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRevisionsAsyncPager

```
ListRevisionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.revision.ListRevisionsResponse],
],
request: google.cloud.run_v2.types.revision.ListRevisionsRequest,
response: google.cloud.run_v2.types.revision.ListRevisionsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest -->

# Class SubmitBuildRequest (0.14.0)

`SubmitBuildRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for submitting a Build.

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
`parent` |
`str`
Required. The project and location to build in. Location must be a region, e.g., 'us-central1' or 'global' if the global builder is to be used. Format: `projects/{project}/locations/{location}`
|
`storage_source` |
Required. Source for the build. This field is a member of `oneof` _ `source` .
|
`image_uri` |
`str`
Required. Artifact Registry URI to store the built image. |
`buildpack_build` |
Build the source using Buildpacks. This field is a member of `oneof` _ `build_type` .
|
`docker_build` |
Build the source using Docker. This means the source has a Dockerfile. This field is a member of `oneof` _ `build_type` .
|
`service_account` |
`str`
Optional. The service account to use for the build. If not set, the default Cloud Build service account for the project will be used. |
`worker_pool` |
`str`
Optional. Name of the Cloud Build Custom Worker Pool that should be used to build the function. The format of this field is `projects/{project}/locations/{region}/workerPools/{workerPool}`
where `{project}` and `{region}` are the project id and
region respectively where the worker pool is defined and
`{workerPool}` is the short name of the worker pool.
|
`tags` |
`MutableSequence[str]`
Optional. Additional tags to annotate the build. |
`machine_type` |
`str`
Optional. The machine type from default pool to use for the build. If left blank, cloudbuild will use a sensible default. Currently only E2_HIGHCPU_8 is supported. If worker_pool is set, this field will be ignored. |
`release_track` |
`google.api.launch_stage_pb2.LaunchStage`
Optional. The release track of the client that initiated the build request. |
`client` |
`str`
Optional. The client that initiated the build request. |

## Classes

### BuildpacksBuild

`BuildpacksBuild(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Build the source using Buildpacks.

### DockerBuild

`DockerBuild(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Build the source using Docker. This means the source has a Dockerfile.


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesexecution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Execution -->

# Class Execution (0.14.0)

`Execution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Execution represents the configuration of a single execution. A execution an immutable resource that references a container image which is run to completion.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The unique name of this Execution. |
`uid` |
`str`
Output only. Server assigned unique identifier for the Execution. The value is a UUID4 string and guaranteed to remain unchanged until the resource is deleted. |
`creator` |
`str`
Output only. Email address of the authenticated creator. |
`generation` |
`int`
Output only. A number that monotonically increases every time the user modifies the desired state. |
`labels` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels |
`annotations` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the execution was acknowledged by the execution controller. It is not guaranteed to be set in happens-before order across separate operations. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the execution started to run. It is not guaranteed to be set in happens-before order across separate operations. |
`completion_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Represents time when the execution was completed. It is not guaranteed to be set in happens-before order across separate operations. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The last-modified time. |
`delete_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the deletion time. It is only populated as a response to a Delete request. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the time after which it will be permamently deleted. It is only populated as a response to a Delete request. |
`launch_stage` |
`google.api.launch_stage_pb2.LaunchStage`
The least stable launch stage needed to create this resource, as defined by `Google Cloud Platform Launch Stages |
`job` |
`str`
Output only. The name of the parent Job. |
`parallelism` |
`int`
Output only. Specifies the maximum desired number of tasks the execution should run at any given time. Must be <= task_count.="" the="" actual="" number="" of="" tasks="" running="" in="" steady="" state="" will="" be="" less="" than="" this="" number="" when="" ((.spec.task_count="" -="" .status.successful)="">< .spec.parallelism),="" i.e.="" when="" the="" work="" left="" to="" do="" is="" less="" than="" max="" parallelism.=""> |
`task_count` |
`int`
Output only. Specifies the desired number of tasks the execution should run. Setting to 1 means that parallelism is limited to 1 and the success of that task signals the success of the execution. |
`template` |
Output only. The template used to create tasks for this execution. |
`reconciling` |
`bool`
Output only. Indicates whether the resource's reconciliation is still in progress. See comments in `Job.reconciling`
for additional information on reconciliation process in
Cloud Run.
|
`conditions` |
`MutableSequence[`
Output only. The Condition of this Execution, containing its readiness status, and detailed error information in case it did not reach the desired state. |
`observed_generation` |
`int`
Output only. The generation of this Execution. See comments in `reconciling` for additional information on
reconciliation process in Cloud Run.
|
`running_count` |
`int`
Output only. The number of actively running tasks. |
`succeeded_count` |
`int`
Output only. The number of tasks which reached phase Succeeded. |
`failed_count` |
`int`
Output only. The number of tasks which reached phase Failed. |
`cancelled_count` |
`int`
Output only. The number of tasks which reached phase Cancelled. |
`retried_count` |
`int`
Output only. The number of tasks which have retried at least once. |
`log_uri` |
`str`
Output only. URI where logs for this execution can be found in Cloud Console. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`etag` |
`str`
Output only. A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

## Classes

### AnnotationsEntry

`AnnotationsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
