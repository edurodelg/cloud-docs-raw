---
merged_at: 2026-02-01T07:56:51.502240
merged_files: 2
---


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
