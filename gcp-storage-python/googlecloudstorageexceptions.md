---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.exceptions
fetched_at: 2026-02-06T16:57:06.535455
---

# Module exceptions (3.8.0)

Exceptions raised by the library.

## Classes

[InvalidResponse](/python/docs/reference/storage/latest/google.cloud.storage.exceptions.InvalidResponse)

`InvalidResponse(response, *args)`


Error class for responses which are not in the correct state.

Parameters |
|
|---|---|
Name |
Description |
`response` |
`object`
The HTTP response which caused the failure. |
`args` |
`tuple`
The positional arguments typically passed to an exception class. |

[DataCorruption](/python/docs/reference/storage/latest/google.cloud.storage.exceptions.DataCorruption)

`DataCorruption(response, *args)`


Error class for corrupt media transfers.

Parameters |
|
|---|---|
Name |
Description |
`response` |
`object`
The HTTP response which caused the failure. |
`args` |
`tuple`
The positional arguments typically passed to an exception class. |