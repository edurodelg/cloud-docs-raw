---
merged_at: 2026-01-28T07:24:29.856546
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionTemplate -->

# Class ExecutionTemplate (0.14.0)

`ExecutionTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ExecutionTemplate describes the data an execution should have when created from a template.

## Attributes |
|
|---|---|
Name |
Description |
`labels` |
`MutableMapping[str, str]`
Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. .. raw:: html Cloud Run API v2 does not support labels with |
`annotations` |
`MutableMapping[str, str]`
Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. .. raw:: html Cloud Run API v2 does not support annotations with This field follows Kubernetes annotations' namespacing, limits, and rules. |
`parallelism` |
`int`
Optional. Specifies the maximum desired number of tasks the execution should run at given time. When the job is run, if this field is 0 or unset, the maximum possible value will be used for that execution. The actual number of tasks running in steady state will be less than this number when there are fewer tasks waiting to be completed remaining, i.e. when the work left to do is less than max parallelism. |
`task_count` |
`int`
Specifies the desired number of tasks the execution should run. Setting to 1 means that parallelism is limited to 1 and the success of that task signals the success of the execution. Defaults to 1. |
`template` |
Required. Describes the task(s) that will be created when executing an execution. |

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.pagers -->

# Module pagers (0.14.0)

API documentation for `run_v2.services.jobs.pagers`

module.

## Classes

[ListJobsAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.pagers.ListJobsAsyncPager)

```
ListJobsAsyncPager(
method: typing.Callable[
[...], typing.Awaitable[google.cloud.run_v2.types.job.ListJobsResponse]
],
request: google.cloud.run_v2.types.job.ListJobsRequest,
response: google.cloud.run_v2.types.job.ListJobsResponse,
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


A pager for iterating through `list_jobs`

requests.

This class thinly wraps an initial
[ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListJobs`

requests and continue to iterate
through the `jobs`

field on the
corresponding responses.

All the usual [ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListJobsPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.pagers.ListJobsPager)

```
ListJobsPager(
method: typing.Callable[[...], google.cloud.run_v2.types.job.ListJobsResponse],
request: google.cloud.run_v2.types.job.ListJobsRequest,
response: google.cloud.run_v2.types.job.ListJobsResponse,
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


A pager for iterating through `list_jobs`

requests.

This class thinly wraps an initial
[ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListJobs`

requests and continue to iterate
through the `jobs`

field on the
corresponding responses.

All the usual [ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Execution -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling -->

# Class ServiceScaling (0.14.0)

`ServiceScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaling settings applied at the service level rather than at the revision level.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`min_instance_count` |
`int`
Optional. total min instances for the service. This number of instances is divided among all revisions with specified traffic based on the percent of traffic they are receiving. |
`scaling_mode` |
Optional. The scaling mode for the service. |
`max_instance_count` |
`int`
Optional. total max instances for the service. This number of instances is divided among all revisions with specified traffic based on the percent of traffic they are receiving. |
`manual_instance_count` |
`int`
Optional. total instance count for the service in manual scaling mode. This number of instances is divided among all revisions with specified traffic based on the percent of traffic they are receiving. This field is a member of `oneof` _ `_manual_instance_count` .
|

## Classes

### ScalingMode

`ScalingMode(value)`


The scaling mode for the service. If not provided, it defaults to AUTOMATIC.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateJobRequest -->

# Class UpdateJobRequest (0.14.0)

`UpdateJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a Job.

## Attributes |
|
|---|---|
Name |
Description |
`job` |
Required. The Job to be updated. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the Job does not exist, it will create a new one. Caller must have both create and update permissions for this call if this is set to true. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretKeySelector -->

# Class SecretKeySelector (0.14.0)

`SecretKeySelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SecretEnvVarSource represents a source for the value of an EnvVar.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret_name} if the secret is in the same project. projects/{project}/secrets/{secret_name} if the secret is in a different project. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers -->

# Module pagers (0.14.0)

API documentation for `run_v2.services.tasks.pagers`

module.

## Classes

[ListTasksAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksAsyncPager)

```
ListTasksAsyncPager(
method: typing.Callable[
[...], typing.Awaitable[google.cloud.run_v2.types.task.ListTasksResponse]
],
request: google.cloud.run_v2.types.task.ListTasksRequest,
response: google.cloud.run_v2.types.task.ListTasksResponse,
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


A pager for iterating through `list_tasks`

requests.

This class thinly wraps an initial
[ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse) object, and
provides an `__aiter__`

method to iterate through its
`tasks`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTasks`

requests and continue to iterate
through the `tasks`

field on the
corresponding responses.

All the usual [ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTasksPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksPager)

```
ListTasksPager(
method: typing.Callable[[...], google.cloud.run_v2.types.task.ListTasksResponse],
request: google.cloud.run_v2.types.task.ListTasksRequest,
response: google.cloud.run_v2.types.task.ListTasksResponse,
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


A pager for iterating through `list_tasks`

requests.

This class thinly wraps an initial
[ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse) object, and
provides an `__iter__`

method to iterate through its
`tasks`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTasks`

requests and continue to iterate
through the `tasks`

field on the
corresponding responses.

All the usual [ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceMesh -->

# Class ServiceMesh (0.14.0)

str
The Mesh resource name. Format:
projects/{project}/locations/global/meshes/{mesh}, where
{project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse -->

# Class ListRevisionsResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListRevisions request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse -->

# Class ListExecutionsResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListExecutions request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse -->

# Class ListWorkerPoolsResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListWorkerPools request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.RevisionReason -->

# Class RevisionReason (0.14.0)

`RevisionReason(value)`


Reasons specific to Revision resource.

## Enums |
|
|---|---|
Name |
Description |
`REVISION_REASON_UNDEFINED` |
Default value. |
`PENDING` |
Revision in Pending state. |
`RESERVE` |
Revision is in Reserve state. |
`RETIRED` |
Revision is Retired. |
`RETIRING` |
Revision is being retired. |
`RECREATING` |
Revision is being recreated. |
`HEALTH_CHECK_CONTAINER_ERROR` |
There was a health check error. |
`CUSTOMIZED_PATH_RESPONSE_PENDING` |
Health check failed due to user error from customized path of the container. System will retry. |
`MIN_INSTANCES_NOT_PROVISIONED` |
A revision with min_instance_count > 0 was created and is reserved, but it was not configured to serve traffic, so it's not live. This can also happen momentarily during traffic migration. |
`ACTIVE_REVISION_LIMIT_REACHED` |
The maximum allowed number of active revisions has been reached. |
`NO_DEPLOYMENT` |
There was no deployment defined. This value is no longer used, but Services created in older versions of the API might contain this value. |
`HEALTH_CHECK_SKIPPED` |
A revision's container has no port specified since the revision is of a manually scaled service with 0 instance count |
`MIN_INSTANCES_WARMING` |
A revision with min_instance_count > 0 was created and is waiting for enough instances to begin a traffic migration. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Volume -->

# Class Volume (0.14.0)

`Volume(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Volume represents a named volume in a container.

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
`name` |
`str`
Required. Volume's name. |
`secret` |
Secret represents a secret that should populate this volume. This field is a member of `oneof` _ `volume_type` .
|
`cloud_sql_instance` |
For Cloud SQL volumes, contains the specific instances that should be mounted. Visit https://cloud.google.com/sql/docs/mysql/connect-run for more information on how to connect Cloud SQL and Cloud Run. This field is a member of `oneof` _ `volume_type` .
|
`empty_dir` |
Ephemeral storage used as a shared volume. This field is a member of `oneof` _ `volume_type` .
|
`nfs` |
For NFS Voumes, contains the path to the nfs Volume This field is a member of `oneof` _ `volume_type` .
|
`gcs` |
Persistent storage backed by a Google Cloud Storage bucket. This field is a member of `oneof` _ `volume_type` .
|
