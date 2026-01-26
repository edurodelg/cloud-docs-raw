---
merged_at: 2026-01-26T23:13:32.269809
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.HTTPGetAction -->

# Class HTTPGetAction (0.14.0)

`HTTPGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HTTPGetAction describes an action based on HTTP Get requests.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Optional. Path to access on the HTTP server. Defaults to '/'. |
`http_headers` |
`MutableSequence[`
Optional. Custom headers to set in the request. HTTP allows repeated headers. |
`port` |
`int`
Optional. Port number to access on the container. Must be in the range 1 to 65535. If not specified, defaults to the exposed port of the container, which is the value of container.ports[0].containerPort. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.Overrides.ContainerOverride -->

# Class ContainerOverride (0.14.0)

`ContainerOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per-container override specification.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the container specified as a DNS_LABEL. |
`args` |
`MutableSequence[str]`
Optional. Arguments to the entrypoint. Will replace existing args for override. |
`env` |
`MutableSequence[`
List of environment variables to set in the container. Will be merged with existing env for override. |
`clear_args` |
`bool`
Optional. True if the intention is to clear out existing args list. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SourceCode -->

# Class SourceCode (0.14.0)

`SourceCode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source type for the container.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`cloud_storage_source` |
The source is a Cloud Storage bucket. This field is a member of `oneof` _ `source_type` .
|

## Classes

### CloudStorageSource

`CloudStorageSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Cloud Storage source.

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.StorageSource -->

# Class StorageSource (0.14.0)

`StorageSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Location of the source in an archive file in Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`bucket` |
`str`
Required. Google Cloud Storage bucket containing the source (see `Bucket Name Requirements |
`object_` |
`str`
Required. Google Cloud Storage object containing the source. This object must be a gzipped archive file ( `.tar.gz` )
containing source to build.
|
`generation` |
`int`
Optional. Google Cloud Storage generation for the object. If the generation is omitted, the latest generation will be used. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers -->

# Module pagers (0.14.0)

API documentation for `run_v2.services.revisions.pagers`

module.

## Classes

[ListRevisionsAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers.ListRevisionsAsyncPager)

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

[ListRevisionsPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers.ListRevisionsPager)

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
