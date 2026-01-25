---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.batch
fetched_at: 2026-01-25T12:21:05.118336
---

# Module batch (3.7.0)

Batch updates / deletes of storage buckets / blobs.

A batch request is a single standard HTTP request containing multiple Cloud Storage JSON API calls. Within this main HTTP request, there are multiple parts which each contain a nested HTTP request. The body of each part is itself a complete HTTP request, with its own verb, URL, headers, and body.

Note that Cloud Storage does not support batch operations for uploading or downloading.
Additionally, the current batch design does not support library methods whose return values
depend on the response payload. See more details in the [Sending Batch Requests official guide](https://cloud.google.com/storage/docs/batch).

Examples of situations when you might want to use the Batch module:
`blob.patch()`

`blob.update()`

`blob.delete()`

`bucket.delete_blob()`

`bucket.patch()`

`bucket.update()`


## Classes

[Batch](/python/docs/reference/storage/latest/google.cloud.storage.batch.Batch)

`Batch(client, raise_exception=True)`


Proxy an underlying connection, batching up change operations.

Parameters |
|
|---|---|
Name |
Description |
`client` |
The client to use for making connections. |
`raise_exception` |
`bool`
(Optional) Defaults to True. If True, instead of adding exceptions to the list of return responses, the final exception will be raised. Note that exceptions are unwrapped after all operations are complete in success or failure, and only the last exception is raised. |

[MIMEApplicationHTTP](/python/docs/reference/storage/latest/google.cloud.storage.batch.MIMEApplicationHTTP)

`MIMEApplicationHTTP(method, uri, headers, body)`


MIME type for `application/http`

.

Constructs payload from headers and body

Parameters |
|
|---|---|
Name |
Description |
`method` |
`str`
HTTP method |
`uri` |
`str`
URI for HTTP request |
`headers` |
`dict`
HTTP headers |
`body` |
`str`
(Optional) HTTP payload |