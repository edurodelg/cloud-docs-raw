---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.fileio.BlobReader
fetched_at: 2026-02-04T00:29:22.823665
---

# Class BlobReader (3.8.0)

```
BlobReader(
blob,
chunk_size=None,
retry=google.api_core.retry.retry_unary.Retry,
**download_kwargs
)
```


A file-like object that reads from a blob.

## Parameters |
|
|---|---|
Name |
Description |
`download_kwargs` |
`dict`
Keyword arguments to pass to the underlying API calls. The following arguments are supported: - |
`blob` |
`'`
The blob to download. |
`chunk_size` |
`long`
(Optional) The minimum number of bytes to read at a time. If fewer bytes than the chunk_size are requested, the remainder is buffered. The default is the chunk_size of the blob, or 40MiB. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |

## Methods

### close

`close()`


Flush and close the IO object.

This method has no effect if the file is already closed.

### read

`read(size=-1)`


Read and return up to n bytes.

If the argument is omitted, None, or negative, reads and returns all data until EOF.

If the argument is positive, and the underlying raw stream is not 'interactive', multiple raw reads may be issued to satisfy the byte count (unless EOF is reached first). But for interactive raw streams (as well as sockets and pipes), at most one raw read will be issued, and a short result does not imply that EOF is imminent.

Returns an empty bytes object on EOF.

Returns None if the underlying raw stream was open in non-blocking mode and no data is available at the moment.

### read1

`read1(size=-1)`


Read and return up to n bytes, with at most one read() call to the underlying raw stream. A short result does not imply that EOF is imminent.

Returns an empty bytes object on EOF.

### readable

`readable()`


Return whether object was opened for reading.

If False, read() will raise OSError.

### seek

`seek(pos, whence=0)`


Seek within the blob.

This implementation of seek() uses knowledge of the blob size to validate that the reported position does not exceed the blob last byte. If the blob size is not already known it will call blob.reload().

### seekable

`seekable()`


Return whether object supports random access.

If False, seek(), tell() and truncate() will raise OSError. This method may need to do a test seek().

### writable

`writable()`


Return whether object was opened for writing.

If False, write() will raise OSError.