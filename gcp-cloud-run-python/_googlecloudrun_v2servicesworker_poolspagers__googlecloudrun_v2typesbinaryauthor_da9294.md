---
merged_at: 2026-01-25T15:25:49.592180
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesworker_poolspagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers -->

# Module pagers (0.14.0)

API documentation for `run_v2.services.worker_pools.pagers`

module.

## Classes

[ListWorkerPoolsAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsAsyncPager)

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

[ListWorkerPoolsPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsPager)

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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesbinaryauthorization_googlecloudrun_v2typesservicescaling.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesbinaryauthorization.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BinaryAuthorization -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesservicescaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling -->

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
