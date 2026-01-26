---
merged_at: 2026-01-26T23:13:32.269304
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitStatus -->

# Class InstanceSplitStatus (0.14.0)

str
Revision to which this instance split is
assigned.

percent

int
Specifies percent of the instance split to
this Revision.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess.VpcEgress -->

# Class VpcEgress (0.14.0)

All outbound traffic is routed through the VPC connector.

PRIVATE_RANGES_ONLY

Only private IP ranges are routed through the VPC connector.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteJobRequest -->

# Class DeleteJobRequest (0.14.0)

`DeleteJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a Job by its full name.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the Job. Format: projects/{project}/locations/{location}/jobs/{job}, where {project} can be project id or number. |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildInfo -->

# Class BuildInfo (0.14.0)

str
Output only. Entry point of the function when
the image is a Cloud Run function.

source_location

str
Output only. Source code location of the
image.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers -->

# Module pagers (0.14.0)

API documentation for `run_v2.services.services.pagers`

module.

## Classes

[ListServicesAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers.ListServicesAsyncPager)

```
ListServicesAsyncPager(
method: typing.Callable[
[...], typing.Awaitable[google.cloud.run_v2.types.service.ListServicesResponse]
],
request: google.cloud.run_v2.types.service.ListServicesRequest,
response: google.cloud.run_v2.types.service.ListServicesResponse,
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


A pager for iterating through `list_services`

requests.

This class thinly wraps an initial
[ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse) object, and
provides an `__aiter__`

method to iterate through its
`services`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListServices`

requests and continue to iterate
through the `services`

field on the
corresponding responses.

All the usual [ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListServicesPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers.ListServicesPager)

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
