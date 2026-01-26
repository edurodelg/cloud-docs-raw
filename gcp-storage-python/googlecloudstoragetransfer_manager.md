---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager
fetched_at: 2026-01-26T23:15:35.525093
---

# Module transfer_manager (3.7.0)

Concurrent media operations.

## Modules Functions

### download_chunks_concurrently

```
download_chunks_concurrently(
blob,
filename,
chunk_size=33554432,
download_kwargs=None,
deadline=None,
worker_type="process",
max_workers=8,
*,
crc32c_checksum=True
)
```


Download a single file in chunks, concurrently.

In some environments, using this feature with mutiple processes will result in faster downloads of large files.

Using this feature with multiple threads is unlikely to improve download performance under normal circumstances due to Python interpreter threading behavior. The default is therefore to use processes instead of threads.

Parameters |
|
|---|---|
Name |
Description |
`blob` |
The blob to be downloaded. |
`filename` |
`str`
The destination filename or path. |
`chunk_size` |
`int`
The size in bytes of each chunk to send. The optimal chunk size for maximum throughput may vary depending on the exact network environment and size of the blob. |
`download_kwargs` |
`dict`
A dictionary of keyword arguments to pass to the download method. Refer to the documentation for |
`deadline` |
`int`
The number of seconds to wait for all threads to resolve. If the deadline is reached, all threads will be terminated regardless of their progress and |
`worker_type` |
`str`
The worker type to use; one of |
`max_workers` |
`int`
The maximum number of workers to create to handle the workload. With PROCESS workers, a larger number of workers will consume more system resources (memory and CPU) at once. How many workers is optimal depends heavily on the specific use case, and the default is a conservative number that should work okay in most cases without consuming excessive resources. |
`crc32c_checksum` |
`bool`
Whether to compute a checksum for the resulting object, using the crc32c algorithm. As the checksums for each chunk must be combined using a feature of crc32c that is not available for md5, md5 is not supported. |

Exceptions |
|
|---|---|
Type |
Description |
``concurrent.futures.TimeoutError` |
if deadline is exceeded. DataCorruption if the download's checksum doesn't agree with server-computed checksum. The `google.cloud.storage._media` exception is used here for consistency with other download methods despite the exception originating elsewhere. |

### download_many

```
download_many(
blob_file_pairs,
download_kwargs=None,
threads=None,
deadline=None,
raise_exception=False,
worker_type="process",
max_workers=8,
*,
skip_if_exists=False
)
```


Download many blobs concurrently via a worker pool.

Exceptions |
|
|---|---|
Type |
Description |
``concurrent.futures.TimeoutError` |
if deadline is exceeded. |

Returns |
|
|---|---|
Type |
Description |
`list` |
A list of results corresponding to, in order, each item in the input list. If an exception was received, it will be the result for that operation. Otherwise, the return value from the successful download method is used (which will be None). |

### download_many_to_path

```
download_many_to_path(
bucket,
blob_names,
destination_directory="",
blob_name_prefix="",
download_kwargs=None,
threads=None,
deadline=None,
create_directories=True,
raise_exception=False,
worker_type="process",
max_workers=8,
*,
skip_if_exists=False
)
```


Download many files concurrently by their blob names.

The destination files are automatically created, with paths based on the source blob_names and the destination_directory.

The destination files are not automatically deleted if their downloads fail,
so please check the return value of this function for any exceptions, or
enable `raise_exception=True`

, and process the files accordingly.

For example, if the `blob_names`

include "icon.jpg", `destination_directory`

is "/home/myuser/", and `blob_name_prefix`

is "images/", then the blob named
"images/icon.jpg" will be downloaded to a file named
"/home/myuser/icon.jpg".

Exceptions |
|
|---|---|
Type |
Description |
``concurrent.futures.TimeoutError` |
if deadline is exceeded. |

Returns |
|
|---|---|
Type |
Description |
`list` |
A list of results corresponding to, in order, each item in the input list. If an exception was received, it will be the result for that operation. Otherwise, the return value from the successful download method is used (which will be None). |

### upload_chunks_concurrently

```
upload_chunks_concurrently(
filename,
blob,
content_type=None,
chunk_size=33554432,
deadline=None,
worker_type="process",
max_workers=8,
*,
checksum="auto",
timeout=60,
retry=google.api_core.retry.retry_unary.Retry
)
```


Upload a single file in chunks, concurrently.

This function uses the XML MPU API to initialize an upload and upload a file in chunks, concurrently with a worker pool.

The XML MPU API is significantly different from other uploads; please review
the documentation at `https://cloud.google.com/storage/docs/multipart-uploads`

before using this feature.

The library will attempt to cancel uploads that fail due to an exception.
If the upload fails in a way that precludes cancellation, such as a
hardware failure, process termination, or power outage, then the incomplete
upload may persist indefinitely. To mitigate this, set the
`AbortIncompleteMultipartUpload`

with a nonzero `Age`

in bucket lifecycle
rules, or refer to the XML API documentation linked above to learn more
about how to list and delete individual downloads.

Using this feature with multiple threads is unlikely to improve upload performance under normal circumstances due to Python interpreter threading behavior. The default is therefore to use processes instead of threads.

ACL information cannot be sent with this function and should be set
separately with `ObjectACL`

methods.

Parameters |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the file to upload. File-like objects are not supported. |
`blob` |
The blob to which to upload. |
`content_type` |
`str`
(Optional) Type of content being uploaded. |
`chunk_size` |
`int`
The size in bytes of each chunk to send. The optimal chunk size for maximum throughput may vary depending on the exact network environment and size of the blob. The remote API has restrictions on the minimum and maximum size allowable, see: |
`deadline` |
`int`
The number of seconds to wait for all threads to resolve. If the deadline is reached, all threads will be terminated regardless of their progress and |
`worker_type` |
`str`
The worker type to use; one of |
`max_workers` |
`int`
The maximum number of workers to create to handle the workload. With PROCESS workers, a larger number of workers will consume more system resources (memory and CPU) at once. How many workers is optimal depends heavily on the specific use case, and the default is a conservative number that should work okay in most cases without consuming excessive resources. |
`checksum` |
`str`
(Optional) The checksum scheme to use: either "md5", "crc32c", "auto" or None. The default is "auto", which will try to detect if the C extension for crc32c is installed and fall back to md5 otherwise. Each individual part is checksummed. At present, the selected checksum rule is only applied to parts and a separate checksum of the entire resulting blob is not computed. Please compute and compare the checksum of the file to the resulting blob separately if needed, using the "crc32c" algorithm as per the XML MPU documentation. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry`
(Optional) How to retry the RPC. A None value will disable retries. A |

Exceptions |
|
|---|---|
Type |
Description |
``concurrent.futures.TimeoutError` |
if deadline is exceeded. |

### upload_many

```
upload_many(
file_blob_pairs,
skip_if_exists=False,
upload_kwargs=None,
threads=None,
deadline=None,
raise_exception=False,
worker_type="process",
max_workers=8,
)
```


Upload many files concurrently via a worker pool.

Exceptions |
|
|---|---|
Type |
Description |
``concurrent.futures.TimeoutError` |
if deadline is exceeded. |

Returns |
|
|---|---|
Type |
Description |
`list` |
A list of results corresponding to, in order, each item in the input list. If an exception was received, it will be the result for that operation. Otherwise, the return value from the successful upload method is used (which will be None). |

### upload_many_from_filenames

```
upload_many_from_filenames(
bucket,
filenames,
source_directory="",
blob_name_prefix="",
skip_if_exists=False,
blob_constructor_kwargs=None,
upload_kwargs=None,
threads=None,
deadline=None,
raise_exception=False,
worker_type="process",
max_workers=8,
*,
additional_blob_attributes=None
)
```


Upload many files concurrently by their filenames.

The destination blobs are automatically created, with blob names based on the source filenames and the blob_name_prefix.

For example, if the `filenames`

include "images/icon.jpg",
`source_directory`

is "/home/myuser/", and `blob_name_prefix`

is "myfiles/",
then the file at "/home/myuser/images/icon.jpg" will be uploaded to a blob
named "myfiles/images/icon.jpg".

Exceptions |
|
|---|---|
Type |
Description |
``concurrent.futures.TimeoutError` |
if deadline is exceeded. |

Returns |
|
|---|---|
Type |
Description |
`list` |
A list of results corresponding to, in order, each item in the input list. If an exception was received, it will be the result for that operation. Otherwise, the return value from the successful upload method is used (which will be None). |