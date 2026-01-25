---
merged_at: 2026-01-25T12:06:29.182456
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesexecutionspagerslistexecutionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers.ListExecutionsAsyncPager -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesworker_poolspagerslistworkerpoolsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsAsyncPager -->

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
