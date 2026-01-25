---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.batch.Batch
fetched_at: 2026-01-25T12:21:08.240139
---

# Class Batch (3.7.0)

`Batch(client, raise_exception=True)`


Proxy an underlying connection, batching up change operations.

## Parameters |
|
|---|---|
Name |
Description |
`client` |
The client to use for making connections. |
`raise_exception` |
`bool`
(Optional) Defaults to True. If True, instead of adding exceptions to the list of return responses, the final exception will be raised. Note that exceptions are unwrapped after all operations are complete in success or failure, and only the last exception is raised. |

## Methods

### current

`current()`


Return the topmost batch, or None.

### finish

`finish(raise_exception=True)`


Submit a single `multipart/mixed`

request with deferred requests.

Parameter |
|
|---|---|
Name |
Description |
`raise_exception` |
`bool`
(Optional) Defaults to True. If True, instead of adding exceptions to the list of return responses, the final exception will be raised. Note that exceptions are unwrapped after all operations are complete in success or failure, and only the last exception is raised. |

Returns |
|
|---|---|
Type |
Description |
`list of tuples` |
one `(headers, payload)` tuple per deferred request. |