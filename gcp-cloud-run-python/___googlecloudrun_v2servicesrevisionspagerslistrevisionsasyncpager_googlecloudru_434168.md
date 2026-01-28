---
merged_at: 2026-01-28T07:24:29.855635
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers.ListRevisionsAsyncPager -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers.ListExecutionsAsyncPager -->

# Class ListExecutionsAsyncPager (0.14.0)

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.execution.ListExecutionsResponse],
],
request: google.cloud.run_v2.types.execution.ListExecutionsRequest,
response: google.cloud.run_v2.types.execution.ListExecutionsResponse,
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
[ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse) object, and
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

All the usual [ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExecutionsAsyncPager

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.execution.ListExecutionsResponse],
],
request: google.cloud.run_v2.types.execution.ListExecutionsRequest,
response: google.cloud.run_v2.types.execution.ListExecutionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/multiprocessing -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SourceCode.CloudStorageSource -->

# Class CloudStorageSource (0.14.0)

int
Optional. The Cloud Storage object
generation.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.NFSVolumeSource -->

# Class NFSVolumeSource (0.14.0)

bool
If true, the volume will be mounted as read
only for all mounts.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolScaling -->

# Class WorkerPoolScaling (0.14.0)

`WorkerPoolScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Worker pool scaling settings.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`manual_instance_count` |
`int`
Optional. The total number of instances in manual scaling mode. This field is a member of `oneof` _ `_manual_instance_count` .
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsAsyncPager -->

# Class ListWorkerPoolsAsyncPager (0.14.0)

```
ListWorkerPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse],
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
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


A pager for iterating through `list_worker_pools`

requests.

This class thinly wraps an initial
[ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`worker_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListWorkerPools`

requests and continue to iterate
through the `worker_pools`

field on the
corresponding responses.

All the usual [ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListWorkerPoolsAsyncPager

```
ListWorkerPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse],
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateWorkerPoolRequest -->

# Class UpdateWorkerPoolRequest (0.14.0)

`UpdateWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a worker pool.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. The list of fields to be updated. |
`worker_pool` |
Required. The WorkerPool to be updated. |
`validate_only` |
`bool`
Optional. Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the WorkerPool does not exist, it will create a new one. The caller must have 'run.workerpools.create' permissions if this is set to true and the WorkerPool does not exist. |
`force_new_revision` |
`bool`
Optional. If set to true, a new revision will be created from the template even if the system doesn't detect any changes from the previously deployed revision. This may be useful for cases where the underlying resources need to be recreated or reinitialized. For example if the image is specified by label, but the underlying image digest has changed) or if the container performs deployment initialization work that needs to be performed again. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.DockerBuild -->

# Class DockerBuild (0.14.0)

Build the source using Docker. This means the source has a
Dockerfile.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScalingStatus -->

# Class RevisionScalingStatus (0.14.0)

int
The current number of min instances
provisioned for this revision.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.CommonReason -->

# Class CommonReason (0.14.0)

`CommonReason(value)`


Reasons common to all types of conditions.

## Enums |
|
|---|---|
Name |
Description |
`COMMON_REASON_UNDEFINED` |
Default value. |
`UNKNOWN` |
Reason unknown. Further details will be in message. |
`REVISION_FAILED` |
Revision creation process failed. |
`PROGRESS_DEADLINE_EXCEEDED` |
Timed out waiting for completion. |
`CONTAINER_MISSING` |
The container image path is incorrect. |
`CONTAINER_PERMISSION_DENIED` |
Insufficient permissions on the container image. |
`CONTAINER_IMAGE_UNAUTHORIZED` |
Container image is not authorized by policy. |
`CONTAINER_IMAGE_AUTHORIZATION_CHECK_FAILED` |
Container image policy authorization check failed. |
`ENCRYPTION_KEY_PERMISSION_DENIED` |
Insufficient permissions on encryption key. |
`ENCRYPTION_KEY_CHECK_FAILED` |
Permission check on encryption key failed. |
`SECRETS_ACCESS_CHECK_FAILED` |
At least one Access check on secrets failed. |
`WAITING_FOR_OPERATION` |
Waiting for operation to complete. |
`IMMEDIATE_RETRY` |
System will retry immediately. |
`POSTPONED_RETRY` |
System will retry later; current attempt failed. |
`INTERNAL` |
An internal error occurred. Further information may be in the message. |
`VPC_NETWORK_NOT_FOUND` |
User-provided VPC network was not found. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BinaryAuthorization -->

# Class BinaryAuthorization (0.14.0)

`BinaryAuthorization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Settings for Binary Authorization feature.

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
`use_default` |
`bool`
Optional. If True, indicates to use the default project's binary authorization policy. If False, binary authorization will be disabled. This field is a member of `oneof` _ `binauthz_method` .
|
`policy` |
`str`
Optional. The path to a binary authorization policy. Format: `projects/{project}/platforms/cloudRun/{policy-name}`
This field is a member of `oneof` _ `binauthz_method` .
|
`breakglass_justification` |
`str`
Optional. If present, indicates to use Breakglass using this justification. If use_default is False, then it must be empty. For more information on breakglass, see https://cloud.google.com/binary-authorization/docs/using-breakglass |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScaling -->

# Class RevisionScaling (0.14.0)

`RevisionScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Settings for revision-level scaling settings.

## Attributes |
|
|---|---|
Name |
Description |
`min_instance_count` |
`int`
Optional. Minimum number of serving instances that this resource should have. |
`max_instance_count` |
`int`
Optional. Maximum number of serving instances that this resource should have. When unspecified, the field is set to the server default value of 100. For more information see https://cloud.google.com/run/docs/configuring/max-instances |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse -->

# Class ListJobsResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListJobs request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse -->

# Class ListTasksResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListTasks request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.IngressTraffic -->

# Class IngressTraffic (0.14.0)

Both internal and Google Cloud Load Balancer traffic is allowed.

INGRESS_TRAFFIC_NONE

No ingress traffic is allowed.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
