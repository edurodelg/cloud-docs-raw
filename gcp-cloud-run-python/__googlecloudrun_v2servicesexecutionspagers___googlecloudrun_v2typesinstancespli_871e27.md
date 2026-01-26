---
merged_at: 2026-01-26T20:50:51.805123
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers -->

# Module pagers (0.14.0)

API documentation for `run_v2.services.executions.pagers`

module.

## Classes

[ListExecutionsAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers.ListExecutionsAsyncPager)

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

[ListExecutionsPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.executions.pagers.ListExecutionsPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitAllocationType -->

# Class InstanceSplitAllocationType (0.14.0)

Allocates instances to the Service's latest ready Revision.

INSTANCE_SPLIT_ALLOCATION_TYPE_REVISION

Allocates instances to a Revision by name.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetAllocationType -->

# Class TrafficTargetAllocationType (0.14.0)

Allocates instances to the Service's latest ready Revision.

TRAFFIC_TARGET_ALLOCATION_TYPE_REVISION

Allocates instances to a Revision by name.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteServiceRequest -->

# Class DeleteServiceRequest (0.14.0)

`DeleteServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a Service by its full name.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the Service. Format: projects/{project}/locations/{location}/services/{service}, where {project} can be project id or number. |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPHeader -->

# Class HTTPHeader (0.14.0)

HTTPHeader describes a custom header to be used in HTTP
probes

Attributes

Name

Description

name

str
Required. The header field name

value

str
Optional. The header field value

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsRequest -->

# Class ListJobsRequest (0.14.0)

`ListJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Jobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project to list resources on. Format: projects/{project}/locations/{location}, where {project} can be project id or number. |
`page_size` |
`int`
Maximum number of Jobs to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListJobs. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GRPCAction -->

# Class GRPCAction (0.14.0)

`GRPCAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GRPCAction describes an action involving a GRPC port.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Optional. Port number of the gRPC service. Number must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |
`service` |
`str`
Optional. Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md ). If this is not specified, the default behavior is defined by gRPC. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetStatus -->

# Class TrafficTargetStatus (0.14.0)

int
Specifies percent of the traffic to this
Revision.

tag

str
Indicates the string used in the URI to
exclusively reference this target.

uri

str
Displays the target URI.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTarget -->

# Class TrafficTarget (0.14.0)

`TrafficTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Holds a single traffic routing entry for the Service. Allocations can be done to a specific Revision name, or pointing to the latest Ready Revision.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
The allocation type for this traffic target. |
`revision` |
`str`
Revision to which to send this portion of traffic, if traffic allocation is by revision. |
`percent` |
`int`
Specifies percent of the traffic to this Revision. This defaults to zero if unspecified. |
`tag` |
`str`
Indicates a string to be part of the URI to exclusively reference this target. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers -->

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
