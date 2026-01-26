---
merged_at: 2026-01-26T23:13:32.268332
merged_files: 2
---


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
