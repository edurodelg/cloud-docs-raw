---
merged_at: 2026-01-30T23:52:17.769507
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.pagers.ListJobsAsyncPager -->

# Class ListJobsAsyncPager (0.15.0)

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

## Methods

### ListJobsAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers.ListServicesPager -->

# Class ListServicesPager (0.15.0)

```
ListServicesPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.service.ListServicesResponse
],
request: google.cloud.run_v2.types.service.ListServicesRequest,
response: google.cloud.run_v2.types.service.ListServicesResponse,
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


A pager for iterating through `list_services`

requests.

This class thinly wraps an initial
[ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse) object, and
provides an `__iter__`

method to iterate through its
`services`

field.

If there are more pages, the `__iter__`

method will make additional
`ListServices`

requests and continue to iterate
through the `services`

field on the
corresponding responses.

All the usual [ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListServicesPager

```
ListServicesPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.service.ListServicesResponse
],
request: google.cloud.run_v2.types.service.ListServicesRequest,
response: google.cloud.run_v2.types.service.ListServicesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksAsyncPager -->

# Class ListTasksAsyncPager (0.15.0)

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

## Methods

### ListTasksAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.instances.pagers.ListInstancesPager -->

# Class ListInstancesPager (0.15.0)

```
ListInstancesPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.instance.ListInstancesResponse
],
request: google.cloud.run_v2.types.instance.ListInstancesRequest,
response: google.cloud.run_v2.types.instance.ListInstancesResponse,
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


A pager for iterating through `list_instances`

requests.

This class thinly wraps an initial
[ListInstancesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListInstancesResponse) object, and
provides an `__iter__`

method to iterate through its
`instances`

field.

If there are more pages, the `__iter__`

method will make additional
`ListInstances`

requests and continue to iterate
through the `instances`

field on the
corresponding responses.

All the usual [ListInstancesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListInstancesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListInstancesPager

```
ListInstancesPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.instance.ListInstancesResponse
],
request: google.cloud.run_v2.types.instance.ListInstancesRequest,
response: google.cloud.run_v2.types.instance.ListInstancesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers.ListRevisionsPager -->

# Class ListRevisionsPager (0.15.0)

```
ListRevisionsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.revision.ListRevisionsResponse
],
request: google.cloud.run_v2.types.revision.ListRevisionsRequest,
response: google.cloud.run_v2.types.revision.ListRevisionsResponse,
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


A pager for iterating through `list_revisions`

requests.

This class thinly wraps an initial
[ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse) object, and
provides an `__iter__`

method to iterate through its
`revisions`

field.

If there are more pages, the `__iter__`

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

### ListRevisionsPager

```
ListRevisionsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.revision.ListRevisionsResponse
],
request: google.cloud.run_v2.types.revision.ListRevisionsRequest,
response: google.cloud.run_v2.types.revision.ListRevisionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs -->

# Package jobs (0.15.0)

API documentation for run_v2.services.jobs.pagers module.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks -->

# Package tasks (0.15.0)

API documentation for run_v2.services.tasks.pagers module.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.Severity -->

# Class Severity (0.15.0)

`Severity(value)`


Represents the severity of the condition failures.

## Enums |
|
|---|---|
Name |
Description |
`SEVERITY_UNSPECIFIED` |
Unspecified severity |
`ERROR` |
Error severity. |
`WARNING` |
Warning severity. |
`INFO` |
Info severity. |

`Severity(value)`


Represents the severity of the condition failures.

## Enums |
|
|---|---|
Name |
Description |
`SEVERITY_UNSPECIFIED` |
Unspecified severity |
`ERROR` |
Error severity. |
`WARNING` |
Warning severity. |
`INFO` |
Info severity. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.services -->

# Package services (0.15.0)

API documentation for run_v2.services.services.pagers module.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers.ListExecutionsPager -->

# Class ListExecutionsPager (0.15.0)

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.execution.ListExecutionsResponse
],
request: google.cloud.run_v2.types.execution.ListExecutionsRequest,
response: google.cloud.run_v2.types.execution.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse) object, and
provides an `__iter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__iter__`

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

### ListExecutionsPager

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.execution.ListExecutionsResponse
],
request: google.cloud.run_v2.types.execution.ListExecutionsRequest,
response: google.cloud.run_v2.types.execution.ListExecutionsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsPager -->

# Class ListWorkerPoolsPager (0.15.0)

```
ListWorkerPoolsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
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


A pager for iterating through `list_worker_pools`

requests.

This class thinly wraps an initial
[ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`worker_pools`

field.

If there are more pages, the `__iter__`

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

### ListWorkerPoolsPager

```
ListWorkerPoolsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types -->

# Package types (0.15.0)

API documentation for `run_v2.types`

package.

## Classes

[BinaryAuthorization](/python/docs/reference/run/latest/google.cloud.run_v2.types.BinaryAuthorization)

Settings for Binary Authorization feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[BuildConfig](/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig)

Describes the Build step of the function that builds a container from the given source.

[BuildInfo](/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildInfo)

Build information of the image.

[CancelExecutionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CancelExecutionRequest)

Request message for deleting an Execution.

[CloudSqlInstance](/python/docs/reference/run/latest/google.cloud.run_v2.types.CloudSqlInstance)

Represents a set of Cloud SQL instances. Each one will be available
under /cloudsql/[instance]. Visit
[https://cloud.google.com/sql/docs/mysql/connect-run](https://cloud.google.com/sql/docs/mysql/connect-run) for more
information on how to connect Cloud SQL and Cloud Run.

[Condition](/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition)

Defines a status condition for a resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[Container](/python/docs/reference/run/latest/google.cloud.run_v2.types.Container)

A single application container. This specifies both the container to run, the command to run in the container and the arguments to supply to it. Note that additional arguments can be supplied by the system to the container at runtime.

[ContainerPort](/python/docs/reference/run/latest/google.cloud.run_v2.types.ContainerPort)

ContainerPort represents a network port in a single container.

[ContainerStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.ContainerStatus)

ContainerStatus holds the information of container name and image digest value.

[CreateInstanceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateInstanceRequest)

[CreateJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateJobRequest)

Request message for creating a Job.

[CreateServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateServiceRequest)

Request message for creating a Service.

[CreateWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateWorkerPoolRequest)

Request message for creating a WorkerPool.

[DeleteExecutionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteExecutionRequest)

Request message for deleting an Execution.

[DeleteInstanceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteInstanceRequest)

[DeleteJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteJobRequest)

Request message to delete a Job by its full name.

[DeleteRevisionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteRevisionRequest)

Request message for deleting a retired Revision. Revision lifecycle is usually managed by making changes to the parent Service. Only retired revisions can be deleted with this API.

[DeleteServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteServiceRequest)

Request message to delete a Service by its full name.

[DeleteWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteWorkerPoolRequest)

Request message to delete a WorkerPool by its full name.

[EmptyDirVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource)

In memory (tmpfs) ephemeral storage. It is ephemeral in the sense that when the sandbox is taken down, the data is destroyed with it (it does not persist across sandbox runs).

[EncryptionKeyRevocationAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.EncryptionKeyRevocationAction)

Specifies behavior if an encryption key used by a resource is revoked.

[EnvVar](/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVar)

EnvVar represents an environment variable present in a Container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[EnvVarSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.EnvVarSource)

EnvVarSource represents a source for the value of an EnvVar.

[Execution](/python/docs/reference/run/latest/google.cloud.run_v2.types.Execution)

Execution represents the configuration of a single execution. A execution an immutable resource that references a container image which is run to completion.

[ExecutionEnvironment](/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionEnvironment)

Alternatives for execution environments.

[ExecutionReference](/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionReference)

Reference to an Execution. Use /Executions.GetExecution with the given name to get full execution including the latest status.

[ExecutionTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionTemplate)

ExecutionTemplate describes the data an execution should have when created from a template.

[GCSVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.GCSVolumeSource)

Represents a volume backed by a Cloud Storage bucket using Cloud Storage FUSE.

[GRPCAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.GRPCAction)

GRPCAction describes an action involving a GRPC port.

[GetExecutionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetExecutionRequest)

Request message for obtaining a Execution by its full name.

[GetInstanceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetInstanceRequest)

[GetJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetJobRequest)

Request message for obtaining a Job by its full name.

[GetRevisionRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetRevisionRequest)

Request message for obtaining a Revision by its full name.

[GetServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetServiceRequest)

Request message for obtaining a Service by its full name.

[GetTaskRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetTaskRequest)

Request message for obtaining a Task by its full name.

[GetWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.GetWorkerPoolRequest)

Request message for obtaining a WorkerPool by its full name.

[HTTPGetAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPGetAction)

HTTPGetAction describes an action based on HTTP Get requests.

[HTTPHeader](/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPHeader)

HTTPHeader describes a custom header to be used in HTTP probes

[IngressTraffic](/python/docs/reference/run/latest/google.cloud.run_v2.types.IngressTraffic)

Allowed ingress traffic for the Container.

[Instance](/python/docs/reference/run/latest/google.cloud.run_v2.types.Instance)

A Cloud Run Instance represents a single group of containers running in a region.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[InstanceSplit](/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplit)

Holds a single instance split entry for the Worker. Allocations can be done to a specific Revision name, or pointing to the latest Ready Revision.

[InstanceSplitAllocationType](/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitAllocationType)

The type of instance split allocation.

[InstanceSplitStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitStatus)

Represents the observed state of a single `InstanceSplit`

entry.

[Job](/python/docs/reference/run/latest/google.cloud.run_v2.types.Job)

Job represents the configuration of a single job, which references a container image that is run to completion.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ListExecutionsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsRequest)

Request message for retrieving a list of Executions.

[ListExecutionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse)

Response message containing a list of Executions.

[ListInstancesRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListInstancesRequest)

Request message for retrieving a list of Instances.

[ListInstancesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListInstancesResponse)

Response message containing a list of Instances.

[ListJobsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsRequest)

Request message for retrieving a list of Jobs.

[ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse)

Response message containing a list of Jobs.

[ListRevisionsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsRequest)

Request message for retrieving a list of Revisions.

[ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse)

Response message containing a list of Revisions.

[ListServicesRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesRequest)

Request message for retrieving a list of Services.

[ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse)

Response message containing a list of Services.

[ListTasksRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksRequest)

Request message for retrieving a list of Tasks.

[ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse)

Response message containing a list of Tasks.

[ListWorkerPoolsRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsRequest)

Request message for retrieving a list of WorkerPools.

[ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse)

Response message containing a list of WorkerPools.

[NFSVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.NFSVolumeSource)

Represents an NFS mount.

[NodeSelector](/python/docs/reference/run/latest/google.cloud.run_v2.types.NodeSelector)

Hardware constraints configuration.

[Probe](/python/docs/reference/run/latest/google.cloud.run_v2.types.Probe)

Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[ResourceRequirements](/python/docs/reference/run/latest/google.cloud.run_v2.types.ResourceRequirements)

ResourceRequirements describes the compute resource requirements.

[Revision](/python/docs/reference/run/latest/google.cloud.run_v2.types.Revision)

A Revision is an immutable snapshot of code and configuration. A Revision references a container image. Revisions are only created by updates to its parent Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RevisionScaling](/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScaling)

Settings for revision-level scaling settings.

[RevisionScalingStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScalingStatus)

Effective settings for the current revision

[RevisionTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionTemplate)

RevisionTemplate describes the data a revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[RunJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest)

Request message to create a new Execution of a Job.

[SecretKeySelector](/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretKeySelector)

SecretEnvVarSource represents a source for the value of an EnvVar.

[SecretVolumeSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretVolumeSource)

The secret's value will be presented as the content of a file whose name is defined in the item path. If no items are defined, the name of the file is the secret.

[Service](/python/docs/reference/run/latest/google.cloud.run_v2.types.Service)

Service acts as a top-level container that manages a set of configurations and revision templates which implement a network service. Service exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership.

[ServiceMesh](/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceMesh)

Settings for Cloud Service Mesh. For more information see
[https://cloud.google.com/service-mesh/docs/overview](https://cloud.google.com/service-mesh/docs/overview).

[ServiceScaling](/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling)

Scaling settings applied at the service level rather than at the revision level.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SourceCode](/python/docs/reference/run/latest/google.cloud.run_v2.types.SourceCode)

Source type for the container.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StartInstanceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.StartInstanceRequest)

Request message for starting an Instance.

[StopInstanceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.StopInstanceRequest)

Request message for deleting an Instance.

[StorageSource](/python/docs/reference/run/latest/google.cloud.run_v2.types.StorageSource)

Location of the source in an archive file in Google Cloud Storage.

[SubmitBuildRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest)

Request message for submitting a Build.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[SubmitBuildResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildResponse)

Response message for submitting a Build.

[TCPSocketAction](/python/docs/reference/run/latest/google.cloud.run_v2.types.TCPSocketAction)

TCPSocketAction describes an action based on opening a socket

[Task](/python/docs/reference/run/latest/google.cloud.run_v2.types.Task)

Task represents a single run of a container to completion.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TaskAttemptResult](/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskAttemptResult)

Result of a task attempt.

[TaskTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskTemplate)

TaskTemplate describes the data a task should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TrafficTarget](/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTarget)

Holds a single traffic routing entry for the Service. Allocations can be done to a specific Revision name, or pointing to the latest Ready Revision.

[TrafficTargetAllocationType](/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetAllocationType)

The type of instance allocation.

[TrafficTargetStatus](/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetStatus)

Represents the observed state of a single `TrafficTarget`

entry.

[UpdateJobRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateJobRequest)

Request message for updating a Job.

[UpdateServiceRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateServiceRequest)

Request message for updating a service.

[UpdateWorkerPoolRequest](/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateWorkerPoolRequest)

Request message for updating a worker pool.

[VersionToPath](/python/docs/reference/run/latest/google.cloud.run_v2.types.VersionToPath)

VersionToPath maps a specific version of a secret to a relative file to mount to, relative to VolumeMount's mount_path.

[Volume](/python/docs/reference/run/latest/google.cloud.run_v2.types.Volume)

Volume represents a named volume in a container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[VolumeMount](/python/docs/reference/run/latest/google.cloud.run_v2.types.VolumeMount)

VolumeMount describes a mounting of a Volume within a container.

[VpcAccess](/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess)

VPC Access settings. For more information on sending traffic
to a VPC network, visit
[https://cloud.google.com/run/docs/configuring/connecting-vpc](https://cloud.google.com/run/docs/configuring/connecting-vpc).

[WorkerPool](/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPool)

WorkerPool acts as a top-level container that manages a set of configurations and revision templates which implement a pull-based workload. WorkerPool exists to provide a singular abstraction which can be access controlled, reasoned about, and which encapsulates software lifecycle decisions such as rollout policy and team resource ownership.

[WorkerPoolRevisionTemplate](/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolRevisionTemplate)

WorkerPoolRevisionTemplate describes the data a worker pool revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[WorkerPoolScaling](/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolScaling)

Worker pool scaling settings.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)
