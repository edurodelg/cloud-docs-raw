---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.fileio.BlobWriter
fetched_at: 2026-01-30T23:53:52.654373
---

# Class BlobWriter (3.8.0)

```
BlobWriter(
blob,
chunk_size=None,
ignore_flush=False,
retry=google.api_core.retry.retry_unary.Retry,
**upload_kwargs
)
```


A file-like object that writes to a blob.

## Parameters |
|
|---|---|
Name |
Description |
`upload_kwargs` |
`dict`
Keyword arguments to pass to the underlying API calls. The following arguments are supported: - |
`blob` |
`'`
The blob to which to write. |
`chunk_size` |
`long`
(Optional) The maximum number of bytes to buffer before sending data to the server, and the size of each request when data is sent. Writes are implemented as a "resumable upload", so chunk_size for writes must be exactly a multiple of 256KiB as with other resumable uploads. The default is the chunk_size of the blob, or 40 MiB. |
`ignore_flush` |
`bool`
Makes flush() do nothing instead of raise an error. flush() without closing is not supported by the remote service and therefore calling it on this class normally results in io.UnsupportedOperation. However, that behavior is incompatible with some consumers and wrappers of file objects in Python, such as zipfile.ZipFile or io.TextIOWrapper. Setting ignore_flush will cause flush() to successfully do nothing, for compatibility with those contexts. The correct way to actually flush data to the remote server is to close() (using this object as a context manager is recommended). |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |

## Methods

### close

`close()`


Flush and close the IO object.

This method has no effect if the file is already closed.

### flush

`flush()`


Flush write buffers, if applicable.

This is not implemented for read-only and non-blocking streams.

### readable

`readable()`


Return whether object was opened for reading.

If False, read() will raise OSError.

### seekable

`seekable()`


Return whether object supports random access.

If False, seek(), tell() and truncate() will raise OSError. This method may need to do a test seek().

### tell

`tell()`


Return current stream position.

### terminate

`terminate()`


Cancel the ResumableUpload.

### writable

`writable()`


Return whether object was opened for writing.

If False, write() will raise OSError.

### write

`write(b)`


Write the given buffer to the IO stream.

Returns the number of bytes written, which is always the length of b in bytes.

Raises BlockingIOError if the buffer is full and the underlying raw stream cannot accept more data at the moment.