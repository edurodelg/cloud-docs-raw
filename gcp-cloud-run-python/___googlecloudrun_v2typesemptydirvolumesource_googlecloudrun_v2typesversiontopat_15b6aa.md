---
merged_at: 2026-01-25T15:25:49.602498
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesemptydirvolumesource_googlecloudrun_v2typesversiontopath_b9d450.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesemptydirvolumesource_googlecloudrun_v2typesversiontopath.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesemptydirvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource -->

# Class EmptyDirVolumeSource (0.14.0)

`EmptyDirVolumeSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


In memory (tmpfs) ephemeral storage. It is ephemeral in the sense that when the sandbox is taken down, the data is destroyed with it (it does not persist across sandbox runs).

## Attributes |
|
|---|---|
Name |
Description |
`medium` |
The medium on which the data is stored. Acceptable values today is only MEMORY or none. When none, the default will currently be backed by memory but could change over time. +optional |
`size_limit` |
`str`
Limit on the storage usable by this EmptyDir volume. The size limit is also applicable for memory medium. The maximum usage on memory medium EmptyDir would be the minimum value between the SizeLimit specified here and the sum of memory limits of all containers. The default is nil which means that the limit is undefined. More info: https://cloud.google.com/run/docs/configuring/in-memory-volumes#configure-volume. Info in Kubernetes: https://kubernetes.io/docs/concepts/storage/volumes/#emptydir |

## Classes

### Medium

`Medium(value)`


The different types of medium supported for EmptyDir.


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesversiontopath.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VersionToPath -->

# Class VersionToPath (0.14.0)

`VersionToPath(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VersionToPath maps a specific version of a secret to a relative file to mount to, relative to VolumeMount's mount_path.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Required. The relative path of the secret in the container. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest value, or an integer or a secret alias for a specific version. |
`mode` |
`int`
Integer octal mode bits to use on this file, must be a value between 01 and 0777 (octal). If 0 or not set, the Volume's default mode will be used. Notes - Internally, a umask of 0222 will be applied to any non-zero value. - This is an integer representation of the mode bits. So, the octal integer value should look exactly as the chmod numeric notation with a leading zero. Some examples: for chmod 640 (u=rw,g=r), set to 0640 (octal) or 416 (base-10). For chmod 755 (u=rwx,g=rx,o=rx), set to 0755 (octal) or 493 (base-10). - This might be in conflict with other options that affect the file mode, like fsGroup, and the result can be other mode bits set. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesexecutiontemplate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionTemplate -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2servicesjobspagers_googlecloudrun_v2servicestaskspagers.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesjobspagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.pagers -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicestaskspagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers -->

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
