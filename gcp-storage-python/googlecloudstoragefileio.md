---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.fileio
fetched_at: 2026-01-30T23:53:46.859433
---

# Module fileio (3.8.0)

Module for file-like access of blobs, usually invoked via Blob.open().

## Classes

[BlobReader](/python/docs/reference/storage/latest/google.cloud.storage.fileio.BlobReader)

```
BlobReader(
blob,
chunk_size=None,
retry=google.api_core.retry.retry_unary.Retry,
**download_kwargs
)
```


A file-like object that reads from a blob.

Parameters |
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

[BlobWriter](/python/docs/reference/storage/latest/google.cloud.storage.fileio.BlobWriter)

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

Parameters |
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

[SlidingBuffer](/python/docs/reference/storage/latest/google.cloud.storage.fileio.SlidingBuffer)

`SlidingBuffer()`


A non-rewindable buffer that frees memory of chunks already consumed.

This class is necessary because `google-resumable-media-python`

expects
`tell()`

to work relative to the start of the file, not relative to a place
in an intermediate buffer. Using this class, we present an external
interface with consistent seek and tell behavior without having to actually
store bytes already sent.

Behavior of this class differs from an ordinary BytesIO buffer. `write()`

will always append to the end of the file only and not change the seek
position otherwise. `flush()`

will delete all data already read (data to the
left of the seek position). `tell()`

will report the seek position of the
buffer including all deleted data. Additionally the class implements
**len**() which will report the size of the actual underlying buffer.

This class does not attempt to implement the entire Python I/O interface.