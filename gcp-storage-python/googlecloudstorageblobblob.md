---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob
fetched_at: 2026-01-30T23:53:08.063100
---

# Class Blob (3.8.0)

```
Blob(
name,
bucket,
chunk_size=None,
encryption_key=None,
kms_key_name=None,
generation=None,
)
```


A wrapper around Cloud Storage's concept of an `Object`

.

## Parameters |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the blob. This corresponds to the unique path of the object in the bucket. If bytes, will be converted to a unicode object. Blob / object names can contain any sequence of valid unicode characters, of length 1-1024 bytes when UTF-8 encoded. |
`bucket` |
The bucket to which this blob belongs. |
`chunk_size` |
`int`
(Optional) The size of a chunk of data whenever iterating (in bytes). This must be a multiple of 256 KB per the API specification. If not specified, the chunk_size of the blob itself is used. If that is not specified, a default value of 40 MB is used. |
`encryption_key` |
`bytes`
(Optional) 32 byte encryption key for customer-supplied encryption. See |
`kms_key_name` |
`str`
(Optional) Resource name of Cloud KMS key used to encrypt the blob's contents. |
`generation` |
`long`
(Optional) If present, selects a specific revision of this object. |

## Properties

### acl

Create our ACL on demand.

### bucket

Bucket which contains the object.

Returns |
|
|---|---|
Type |
Description |
|
The object's bucket. |

### cache_control

Scalar property getter.

### chunk_size

Get the blob's default chunk size.

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The current blob's chunk size, if it is set. |

### client

The client bound to this blob.

### component_count

Number of underlying components that make up this object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The component count (in case of a composed object) or `None` if the blob's resource has not been loaded from the server. This property will not be set on objects not created via `compose` . |

### content_disposition

Scalar property getter.

### content_encoding

Scalar property getter.

### content_language

Scalar property getter.

### content_type

Scalar property getter.

### crc32c

Scalar property getter.

### custom_time

Retrieve the custom time for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the blob's resource has not been loaded from the server (see `reload` ). |

### encryption_key

Retrieve the customer-supplied encryption key for the object.

Returns |
|
|---|---|
Type |
Description |
`bytes or ` |
The encryption key or `None` if no customer-supplied encryption key was used, or the blob's resource has not been loaded from the server. |

### etag

Retrieve the ETag for the object.

See [ RFC 2616 (etags)](https://tools.ietf.org/html/rfc2616#section-3.11) and

[.](https://cloud.google.com/storage/docs/json_api/v1/objects)

`API reference docs`

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The blob etag or `None` if the blob's resource has not been loaded from the server. |

### event_based_hold

Scalar property getter.

### generation

Retrieve the generation for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The generation of the blob or `None` if the blob's resource has not been loaded from the server. |

### hard_delete_time

If this object has been soft-deleted, returns the time at which it will be permanently deleted.

Returns |
|
|---|---|
Type |
Description |
|
(readonly) The time that the object will be permanently deleted. Note this property is only set for soft-deleted objects. |

### id

Retrieve the ID for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

The ID consists of the bucket name, object name, and generation number.

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The ID of the blob or `None` if the blob's resource has not been loaded from the server. |

### kms_key_name

Resource name of Cloud KMS key used to encrypt the blob's contents.

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The resource name or `None` if no Cloud KMS key was used, or the blob's resource has not been loaded from the server. |

### md5_hash

Scalar property getter.

### media_link

Retrieve the media download URI for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The media link for the blob or `None` if the blob's resource has not been loaded from the server. |

### metadata

Retrieve arbitrary/application specific metadata for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

:setter: Update arbitrary/application specific metadata for the object. :getter: Retrieve arbitrary/application specific metadata for the object.

Returns |
|
|---|---|
Type |
Description |
`dict or ` |
The metadata associated with the blob or `None` if the property is not set. |

### metageneration

Retrieve the metageneration for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The metageneration of the blob or `None` if the blob's resource has not been loaded from the server. |

### owner

Retrieve info about the owner of the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`dict or ` |
Mapping of owner's role/ID, or `None` if the blob's resource has not been loaded from the server. |

### path

Getter property for the URL path to this Blob.

Returns |
|
|---|---|
Type |
Description |
`str` |
The URL path to this Blob. |

### public_url

The public URL for this blob.

Use `make_public`

to enable anonymous access via the returned
URL.

Returns |
|
|---|---|
Type |
Description |
|
The public URL for this blob. |

### retention

Retrieve the retention configuration for this object.

Returns |
|
|---|---|
Type |
Description |
|
an instance for managing the object's retention configuration. |

### retention_expiration_time

Retrieve timestamp at which the object's retention period expires.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the property is not set locally. |

### self_link

Retrieve the URI for the object.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The self link for the blob or `None` if the blob's resource has not been loaded from the server. |

### size

Size of the object, in bytes.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The size of the blob or `None` if the blob's resource has not been loaded from the server. |

### soft_delete_time

If this object has been soft-deleted, returns the time at which it became soft-deleted.

Returns |
|
|---|---|
Type |
Description |
|
(readonly) The time that the object became soft-deleted. Note this property is only set for soft-deleted objects. |

### storage_class

Scalar property getter.

### temporary_hold

Scalar property getter.

### time_created

Retrieve the timestamp at which the object was created.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the blob's resource has not been loaded from the server (see `reload` ). |

### time_deleted

Retrieve the timestamp at which the object was deleted.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the blob's resource has not been loaded from the server (see `reload` ). If the blob has not been deleted, this will never be set. |

### updated

Retrieve the timestamp at which the object was updated.

See [https://cloud.google.com/storage/docs/json_api/v1/objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the blob's resource has not been loaded from the server (see `reload` ). |

### user_project

Project ID billed for API requests made via this blob.

Derived from bucket's value.

## Methods

### Blob

```
Blob(
name,
bucket,
chunk_size=None,
encryption_key=None,
kms_key_name=None,
generation=None,
)
```


property `name`

Get the blob's name.

### compose

```
compose(
sources,
client=None,
timeout=60,
if_generation_match=None,
if_metageneration_match=None,
if_source_generation_match=None,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Concatenate source blobs into this one.

If `user_project`

is set on the bucket, bills the API request
to that project.

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/objects/compose)
and a [code sample](https://cloud.google.com/storage/docs/samples/storage-compose-file#storage_compose_file-python).

Parameters |
|
|---|---|
Name |
Description |
`sources` |
`list of `
Blobs whose contents will be composed into this blob. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_generation_match` |
`long`
(Optional) Makes the operation conditional on whether the destination object's current generation matches the given value. Setting to 0 makes the operation succeed only if there are no live versions of the object. Note: In a previous version, this argument worked identically to the |
`if_metageneration_match` |
`long`
(Optional) Makes the operation conditional on whether the destination object's current metageneration matches the given value. If a list of long is passed in, no match operation will be performed. (Deprecated: type(list of long) is supported for backwards-compatability reasons only.) |
`if_source_generation_match` |
`list of long`
(Optional) Makes the operation conditional on whether the current generation of each source blob matches the corresponding generation. The list must match |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. The default value is |

### create_resumable_upload_session

```
create_resumable_upload_session(
content_type=None,
size=None,
origin=None,
client=None,
timeout=60,
checksum="auto",
predefined_acl=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Create a resumable upload session.

Resumable upload sessions allow you to start an upload session from one client and complete the session in another. This method is called by the initiator to set the metadata and limits. The initiator then passes the session URL to the client that will upload the binary data. The client performs a PUT request on the session URL to complete the upload. This process allows untrusted clients to upload to an access-controlled bucket.

For more details, see the
documentation on [ signed URLs](https://cloud.google.com/storage/docs/access-control/signed-urls#signing-resumable).

The content type of the upload will be determined in order of precedence:

- The value passed in to this method (if not :data:
`None`

) - The value stored on the current blob
- The default value ('application/octet-stream')

[and](https://cloud.google.com/storage/docs/object-versioning)

`object versioning`

[API documents for details.](https://cloud.google.com/storage/docs/lifecycle)

`lifecycle`

If `encryption_key`

is set, the blob will be encrypted with
a [ customer-supplied](https://cloud.google.com/storage/docs/encryption#customer-supplied)
encryption key.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`size` |
`int`
(Optional) The maximum number of bytes that can be uploaded using this session. If the size is not known when creating the session, this should be left blank. |
`content_type` |
`str`
(Optional) Type of content being uploaded. |
`origin` |
`str`
(Optional) If set, the upload can only be completed by a user-agent that uploads from the given origin. This can be useful when passing the session to a web client. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. After the upload is complete, the server-computed checksum of the resulting object will be checked and |
`predefined_acl` |
`str`
(Optional) Predefined access control list |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |

Exceptions |
|
|---|---|
Type |
Description |
`GoogleCloudError` |
if the session creation response returns an error status. |

Returns |
|
|---|---|
Type |
Description |
`str` |
The resumable upload session URL. The upload can be completed by making an HTTP PUT request with the file's contents. |

### delete

```
delete(
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Deletes a blob from Cloud Storage.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |
(propagated from
|

### download_as_bytes

```
download_as_bytes(
client=None,
start=None,
end=None,
raw_download=False,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
checksum="auto",
retry=google.api_core.retry.retry_unary.Retry,
single_shot_download=False,
)
```


Download the contents of this blob as a bytes object.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`start` |
`int`
(Optional) The first byte in a range to be downloaded. |
`end` |
`int`
(Optional) The last byte in a range to be downloaded. |
`raw_download` |
`bool`
(Optional) If true, download the object without any expansion. |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. The response headers must contain a checksum of the requested type. If the headers lack an appropriate checksum (for instance in the case of transcoded or ranged downloads where the remote service does not know the correct checksum, including downloads where chunk_size is set) an INFO-level log will be emitted. Supported values are "md5", "crc32c", "auto" and None. The default is "auto", which will try to detect if the C extension for crc32c is installed and fall back to md5 otherwise. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`single_shot_download` |
`bool`
(Optional) If true, download the object in a single request. Caution: Enabling this will increase the memory overload for your application. Please enable this as per your use case. |

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |

Returns |
|
|---|---|
Type |
Description |
`bytes` |
The data stored in this blob. |

### download_as_string

```
download_as_string(
client=None,
start=None,
end=None,
raw_download=False,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
single_shot_download=False,
)
```


(Deprecated) Download the contents of this blob as a bytes object.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`start` |
`int`
(Optional) The first byte in a range to be downloaded. |
`end` |
`int`
(Optional) The last byte in a range to be downloaded. |
`raw_download` |
`bool`
(Optional) If true, download the object without any expansion. |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`single_shot_download` |
`bool`
(Optional) If true, download the object in a single request. Caution: Enabling this will increase the memory overload for your application. Please enable this as per your use case. |

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |

Returns |
|
|---|---|
Type |
Description |
`bytes` |
The data stored in this blob. |

### download_as_text

```
download_as_text(
client=None,
start=None,
end=None,
raw_download=False,
encoding=None,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
single_shot_download=False,
)
```


Download the contents of this blob as text (*not* bytes).

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`start` |
`int`
(Optional) The first byte in a range to be downloaded. |
`end` |
`int`
(Optional) The last byte in a range to be downloaded. |
`raw_download` |
`bool`
(Optional) If true, download the object without any expansion. |
`encoding` |
`str`
(Optional) encoding to be used to decode the downloaded bytes. Defaults to the |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`single_shot_download` |
`bool`
(Optional) If true, download the object in a single request. Caution: Enabling this will increase the memory overload for your application. Please enable this as per your use case. |

Returns |
|
|---|---|
Type |
Description |
`text` |
The data stored in this blob, decoded to text. |

### download_to_file

```
download_to_file(
file_obj,
client=None,
start=None,
end=None,
raw_download=False,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
checksum="auto",
retry=google.api_core.retry.retry_unary.Retry,
single_shot_download=False,
)
```


Download the contents of this blob into a file-like object.

For more fine-grained control over the download process, check out[. For example, this library allows downloading](https://googleapis.dev/python/google-resumable-media/latest/index.html)

`google-resumable-media`

**parts**of a blob rather than the whole thing.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`file_obj` |
`file`
A file handle to which to write the blob's data. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`start` |
`int`
(Optional) The first byte in a range to be downloaded. |
`end` |
`int`
(Optional) The last byte in a range to be downloaded. |
`raw_download` |
`bool`
(Optional) If true, download the object without any expansion. |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. The response headers must contain a checksum of the requested type. If the headers lack an appropriate checksum (for instance in the case of transcoded or ranged downloads where the remote service does not know the correct checksum, including downloads where chunk_size is set) an INFO-level log will be emitted. Supported values are "md5", "crc32c", "auto" and None. The default is "auto", which will try to detect if the C extension for crc32c is installed and fall back to md5 otherwise. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`single_shot_download` |
`bool`
(Optional) If true, download the object in a single request. Caution: Enabling this will increase the memory overload for your application. Please enable this as per your use case. |

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |

### download_to_filename

```
download_to_filename(
filename,
client=None,
start=None,
end=None,
raw_download=False,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
checksum="auto",
retry=google.api_core.retry.retry_unary.Retry,
single_shot_download=False,
)
```


Download the contents of this blob into a named file.

If `user_project`

is set on the bucket, bills the API request
to that project.

See a [code sample](https://cloud.google.com/storage/docs/samples/storage-download-encrypted-file#storage_download_encrypted_file-python)
to download a file with a [ customer-supplied encryption key](https://cloud.google.com/storage/docs/encryption#customer-supplied).

Parameters |
|
|---|---|
Name |
Description |
`filename` |
`str`
A filename to be passed to |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`start` |
`int`
(Optional) The first byte in a range to be downloaded. |
`end` |
`int`
(Optional) The last byte in a range to be downloaded. |
`raw_download` |
`bool`
(Optional) If true, download the object without any expansion. |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. The response headers must contain a checksum of the requested type. If the headers lack an appropriate checksum (for instance in the case of transcoded or ranged downloads where the remote service does not know the correct checksum, including downloads where chunk_size is set) an INFO-level log will be emitted. Supported values are "md5", "crc32c", "auto" and None. The default is "auto", which will try to detect if the C extension for crc32c is installed and fall back to md5 otherwise. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`single_shot_download` |
`bool`
(Optional) If true, download the object in a single request. Caution: Enabling this will increase the memory overload for your application. Please enable this as per your use case. |

Exceptions |
|
|---|---|
Type |
Description |
`NotFound` |

### exists

```
exists(
client=None,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
soft_deleted=None,
)
```


Determines whether or not this blob exists.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`soft_deleted` |
`bool`
(Optional) If True, looks for a soft-deleted object. Will only return True if the object exists and is in a soft-deleted state. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if the blob exists in Cloud Storage. |

### from_string

`from_string(uri, client=None)`


(Deprecated) Get a constructor for blob object by URI.

`from google.cloud import `[storage](https://docs.cloud.google.com/python/docs/reference/storage/latest)
from google.cloud.storage.blob import [Blob](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob.html)
client = [storage](https://docs.cloud.google.com/python/docs/reference/storage/latest).[Client](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client.html)()
blob = [Blob](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob.html).[from_string](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob.html#google_cloud_storage_blob_Blob_from_string)("gs://bucket/object", client=client)


Parameters |
|
|---|---|
Name |
Description |
`uri` |
`str`
The blob uri following a gs://bucket/object pattern. Both a bucket and object name is required to construct a blob object. |
`client` |
(Optional) The client to use. Application code should |

Returns |
|
|---|---|
Type |
Description |
|
The blob object created. |

### from_uri

`from_uri(uri, client=None)`


Get a constructor for blob object by URI.

`from google.cloud import `[storage](https://docs.cloud.google.com/python/docs/reference/storage/latest)
from google.cloud.storage.blob import [Blob](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob.html)
client = [storage](https://docs.cloud.google.com/python/docs/reference/storage/latest).[Client](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client.html)()
blob = [Blob](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob.html).[from_uri](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob.html#google_cloud_storage_blob_Blob_from_uri)("gs://bucket/object", client=client)


Parameters |
|
|---|---|
Name |
Description |
`uri` |
`str`
The blob uri following a gs://bucket/object pattern. Both a bucket and object name is required to construct a blob object. |
`client` |
(Optional) The client to use. Application code should |

Returns |
|
|---|---|
Type |
Description |
|
The blob object created. |

### generate_signed_url

```
generate_signed_url(
expiration=None,
api_access_endpoint=None,
method="GET",
content_md5=None,
content_type=None,
response_disposition=None,
response_type=None,
generation=None,
headers=None,
query_parameters=None,
client=None,
credentials=None,
version=None,
service_account_email=None,
access_token=None,
virtual_hosted_style=False,
bucket_bound_hostname=None,
scheme="http",
)
```


Generates a signed URL for this blob.

See a[code sample](https://cloud.google.com/storage/docs/samples/storage-generate-signed-url-v4#storage_generate_signed_url_v4-python).

This is particularly useful if you don't want publicly accessible blobs, but don't want to require users to explicitly log in.

If `bucket_bound_hostname`

is set as an argument of `api_access_endpoint`

,
`https`

works only if using a `CDN`

.

Parameters |
|
|---|---|
Name |
Description |
`expiration` |
`Union[Integer, datetime.datetime, datetime.timedelta]`
Point in time when the signed URL should expire. If a |
`api_access_endpoint` |
`str`
(Optional) URI base, for instance " |
`method` |
`str`
The HTTP verb that will be used when requesting the URL. |
`content_md5` |
`str`
(Optional) The MD5 hash of the object referenced by |
`content_type` |
`str`
(Optional) The content type of the object referenced by |
`response_disposition` |
`str`
(Optional) Content disposition of responses to requests for the signed URL. For example, to enable the signed URL to initiate a file of |
`response_type` |
`str`
(Optional) Content type of responses to requests for the signed URL. Ignored if content_type is set on object/blob metadata. |
`generation` |
`str`
(Optional) A value that indicates which generation of the resource to fetch. |
`headers` |
`dict`
(Optional) Additional HTTP headers to be included as part of the signed URLs. See: |
`query_parameters` |
`dict`
(Optional) Additional query parameters to be included as part of the signed URLs. See: |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`credentials` |
(Optional) The authorization credentials to attach to requests. These credentials identify this application to the service. If none are specified, the client will attempt to ascertain the credentials from the environment. |
`version` |
`str`
(Optional) The version of signed credential to create. Must be one of 'v2' 'v4'. |
`service_account_email` |
`str`
(Optional) E-mail address of the service account. |
`access_token` |
`str`
(Optional) Access token for a service account. |
`virtual_hosted_style` |
`bool`
(Optional) If true, then construct the URL relative the bucket's virtual hostname, e.g., '
|
`bucket_bound_hostname` |
`str`
(Optional) If passed, then construct the URL relative to the bucket-bound hostname. Value can be a bare or with scheme, e.g., 'example.com' or ' |
`scheme` |
`str`
(Optional) If |

Exceptions |
|
|---|---|
Type |
Description |
``ValueError` |
when version is invalid or mutually exclusive arguments are used. |
``TypeError` |
when expiration is not a valid type. |
``AttributeError` |
if credentials is not an instance of `google.auth.credentials.Signing` . |

Returns |
|
|---|---|
Type |
Description |
`str` |
A signed URL you can use to access the resource until expiration. |

### get_iam_policy

```
get_iam_policy(
client=None,
requested_policy_version=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Retrieve the IAM policy for the object.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`requested_policy_version` |
`int or `
(Optional) The version of IAM policies to request. If a policy with a condition is requested without setting this, the server will return an error. This must be set to a value of 3 to retrieve IAM policies containing conditions. This is to prevent client code that isn't aware of IAM conditions from interpreting and modifying policies incorrectly. The service might return a policy with version lower than the one that was requested, based on the feature syntax in the policy fetched. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Returns |
|
|---|---|
Type |
Description |
|
the policy instance, based on the resource returned from the `getIamPolicy` API request. |

### make_private

```
make_private(
client=None,
timeout=60,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Update blob's ACL, revoking read access for anonymous users.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

### make_public

```
make_public(
client=None,
timeout=60,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Update blob's ACL, granting read access to anonymous users.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

### open

```
open(
mode="r",
chunk_size=None,
ignore_flush=None,
encoding=None,
errors=None,
newline=None,
**kwargs
)
```


Create a file handler for file-like I/O to or from this blob.

This method can be used as a context manager, just like Python's built-in 'open()' function.

While reading, as with other read methods, if blob.generation is not set the most recent blob generation will be used. Because the file-like IO reader downloads progressively in chunks, this could result in data from multiple versions being mixed together. If this is a concern, use either bucket.get_blob(), or blob.reload(), which will download the latest generation number and set it; or, if the generation is known, set it manually, for instance with bucket.blob(generation=123456).

Checksumming (hashing) to verify data integrity is disabled for reads
using this feature because reads are implemented using request ranges,
which do not provide checksums to validate. See
[https://cloud.google.com/storage/docs/hashes-etags](https://cloud.google.com/storage/docs/hashes-etags) for details.

See a [code sample](https://github.com/googleapis/python-storage/blob/main/samples/snippets/storage_fileio_write_read.py).

Keyword arguments to pass to the underlying API calls. For both uploads and downloads, the following arguments are supported:

`if_generation_match`

`if_generation_not_match`

`if_metageneration_match`

`if_metageneration_not_match`

`timeout`

`retry`


For downloads only, the following additional arguments are supported:

`raw_download`

`single_shot_download`


For uploads only, the following additional arguments are supported:

`content_type`

`predefined_acl`

`checksum`


Parameters |
|
|---|---|
Name |
Description |
`mode` |
`str`
(Optional) A mode string, as per standard Python |
`chunk_size` |
`long`
(Optional) For reads, the minimum number of bytes to read at a time. If fewer bytes than the chunk_size are requested, the remainder is buffered. For writes, the maximum number of bytes to buffer before sending data to the server, and the size of each request when data is sent. Writes are implemented as a "resumable upload", so chunk_size for writes must be exactly a multiple of 256KiB as with other resumable uploads. The default is 40 MiB. |
`ignore_flush` |
`bool`
(Optional) For non text-mode writes, makes flush() do nothing instead of raising an error. flush() without closing is not supported by the remote service and therefore calling it normally results in io.UnsupportedOperation. However, that behavior is incompatible with some consumers and wrappers of file objects in Python, such as zipfile.ZipFile or io.TextIOWrapper. Setting ignore_flush will cause flush() to successfully do nothing, for compatibility with those contexts. The correct way to actually flush data to the remote server is to close() (using a context manager, such as in the example, will cause this to happen automatically). |
`encoding` |
`str`
(Optional) For text mode only, the name of the encoding that the stream will be decoded or encoded with. If omitted, it defaults to locale.getpreferredencoding(False). |
`errors` |
`str`
(Optional) For text mode only, an optional string that specifies how encoding and decoding errors are to be handled. Pass 'strict' to raise a ValueError exception if there is an encoding error (the default of None has the same effect), or pass 'ignore' to ignore errors. (Note that ignoring encoding errors can lead to data loss.) Other more rarely-used options are also available; see the Python 'io' module documentation for 'io.TextIOWrapper' for a complete list. |
`newline` |
`str`
(Optional) For text mode only, controls how line endings are handled. It can be None, '', '\n', '\r', and '\r\n'. If None, reads use "universal newline mode" and writes use the system default. See the Python 'io' module documentation for 'io.TextIOWrapper' for details. |

### patch

```
patch(
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
override_unlocked_retention=False,
)
```


Sends all changed properties in a PATCH request.

Updates the `_properties`

with the response from the backend.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
the client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`override_unlocked_retention` |
`bool`
(Optional) override_unlocked_retention must be set to True if the operation includes a retention property that changes the mode from Unlocked to Locked, reduces the retainUntilTime, or removes the retention configuration from the object. See: |

### path_helper

`path_helper(bucket_path, blob_name)`


Relative URL path for a blob.

Parameters |
|
|---|---|
Name |
Description |
`bucket_path` |
`str`
The URL path for a bucket. |
`blob_name` |
`str`
The name of the blob. |

Returns |
|
|---|---|
Type |
Description |
`str` |
The relative URL path for `blob_name` . |

### reload

```
reload(
client=None,
projection="noAcl",
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
soft_deleted=None,
)
```


Reload properties from Cloud Storage.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
the client to use. If not passed, falls back to the |
`projection` |
`str`
(Optional) If used, must be 'full' or 'noAcl'. Defaults to |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) See :ref: |
`if_etag_not_match` |
`Union[str, Set[str]])`
(Optional) See :ref: |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`soft_deleted` |
`bool`
(Optional) If True, looks for a soft-deleted object. Will only return the object metadata if the object exists and is in a soft-deleted state. |

### rewrite

```
rewrite(
source,
token=None,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
if_source_generation_match=None,
if_source_generation_not_match=None,
if_source_metageneration_match=None,
if_source_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Rewrite source blob into this one.

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`source` |
blob whose contents will be rewritten into this blob. |
`token` |
`str`
(Optional) Token returned from an earlier, not-completed call to rewrite the same source blob. If passed, result will include updated status, total bytes written. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`if_source_generation_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's generation matches the given value. |
`if_source_generation_not_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's generation does not match the given value. |
`if_source_metageneration_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's current metageneration matches the given value. |
`if_source_metageneration_not_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's current metageneration does not match the given value. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. The default value is |

Returns |
|
|---|---|
Type |
Description |
`tuple` |
`(token, bytes_rewritten, total_bytes)` , where `token` is a rewrite token (`None` if the rewrite is complete), `bytes_rewritten` is the number of bytes rewritten so far, and `total_bytes` is the total number of bytes to be rewritten. |

### set_iam_policy

```
set_iam_policy(
policy,
client=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Update the IAM policy for the bucket.

Parameters |
|
|---|---|
Name |
Description |
`policy` |
policy instance used to update bucket's IAM policy. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Returns |
|
|---|---|
Type |
Description |
|
the policy instance, based on the resource returned from the `setIamPolicy` API request. |

### test_iam_permissions

```
test_iam_permissions(
permissions, client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


API call: test permissions

Parameters |
|
|---|---|
Name |
Description |
`permissions` |
`list of string`
the permissions to check |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Returns |
|
|---|---|
Type |
Description |
`list of string` |
the permissions returned by the `testIamPermissions` API request. |

### update

```
update(
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
override_unlocked_retention=False,
)
```


Sends all properties in a PUT request.

Updates the `_properties`

with the response from the backend.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
the client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`override_unlocked_retention` |
`bool`
(Optional) override_unlocked_retention must be set to True if the operation includes a retention property that changes the mode from Unlocked to Locked, reduces the retainUntilTime, or removes the retention configuration from the object. See: |

### update_storage_class

```
update_storage_class(
new_class,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
if_source_generation_match=None,
if_source_generation_not_match=None,
if_source_metageneration_match=None,
if_source_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Update blob's storage class via a rewrite-in-place. This helper will wait for the rewrite to complete before returning, so it may take some time for large files.

See
[https://cloud.google.com/storage/docs/per-object-storage-class](https://cloud.google.com/storage/docs/per-object-storage-class)

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`new_class` |
`str`
new storage class for the object. One of: NEARLINE_STORAGE_CLASS, COLDLINE_STORAGE_CLASS, ARCHIVE_STORAGE_CLASS, STANDARD_STORAGE_CLASS, MULTI_REGIONAL_LEGACY_STORAGE_CLASS, or REGIONAL_LEGACY_STORAGE_CLASS. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`if_source_generation_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's generation matches the given value. |
`if_source_generation_not_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's generation does not match the given value. |
`if_source_metageneration_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's current metageneration matches the given value. |
`if_source_metageneration_not_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's current metageneration does not match the given value. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. The default value is |

### upload_from_file

```
upload_from_file(
file_obj,
rewind=False,
size=None,
content_type=None,
client=None,
predefined_acl=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
checksum="auto",
retry=google.api_core.retry.retry_unary.Retry,
crc32c_checksum_value=None,
)
```


Upload the contents of this blob from a file-like object.

The content type of the upload will be determined in order of precedence:

- The value passed in to this method (if not :data:
`None`

) - The value stored on the current blob
- The default value ('application/octet-stream')

[and](https://cloud.google.com/storage/docs/object-versioning)

`object versioning`

[API documents for details.](https://cloud.google.com/storage/docs/lifecycle)

`lifecycle`

If the size of the data to be uploaded exceeds 8 MB a resumable media request will be used, otherwise the content and the metadata will be uploaded in a single multipart upload request.

For more fine-grained over the upload process, check out
[ google-resumable-media](https://googleapis.dev/python/google-resumable-media/latest/index.html).

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`file_obj` |
`file`
A file handle opened in binary mode for reading. |
`rewind` |
`bool`
If True, seek to the beginning of the file handle before writing the file to Cloud Storage. |
`size` |
`int`
The number of bytes to be uploaded (which will be read from |
`content_type` |
`str`
(Optional) Type of content being uploaded. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`predefined_acl` |
`str`
(Optional) Predefined access control list |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. If the upload is completed in a single request, the checksum will be entirely precomputed and the remote server will handle verification and error handling. If the upload is too large and must be transmitted in multiple requests, the checksum will be incrementally computed and the client will handle verification and error handling, raising |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`crc32c_checksum_value` |
`str`
(Optional) This should be the checksum of the entire contents of |

Exceptions |
|
|---|---|
Type |
Description |
`GoogleCloudError` |
if the upload response returns an error status. |

### upload_from_filename

```
upload_from_filename(
filename,
content_type=None,
client=None,
predefined_acl=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
checksum="auto",
retry=google.api_core.retry.retry_unary.Retry,
crc32c_checksum_value=None,
)
```


Upload this blob's contents from the content of a named file.

The content type of the upload will be determined in order of precedence:

- The value passed in to this method (if not :data:
`None`

) - The value stored on the current blob
- The value given by
`mimetypes.guess_type`

- The default value ('application/octet-stream')

[and](https://cloud.google.com/storage/docs/object-versioning)

`object versioning`

[API documents for details.](https://cloud.google.com/storage/docs/lifecycle)

`lifecycle`

If `user_project`

is set on the bucket, bills the API request
to that project.

See a [code sample](https://cloud.google.com/storage/docs/samples/storage-upload-encrypted-file#storage_upload_encrypted_file-python)
to upload a file with a
[ customer-supplied encryption key](https://cloud.google.com/storage/docs/encryption#customer-supplied).

Parameters |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the file. |
`content_type` |
`str`
(Optional) Type of content being uploaded. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`predefined_acl` |
`str`
(Optional) Predefined access control list |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. If the upload is completed in a single request, the checksum will be entirely precomputed and the remote server will handle verification and error handling. If the upload is too large and must be transmitted in multiple requests, the checksum will be incrementally computed and the client will handle verification and error handling, raising |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`crc32c_checksum_value` |
`str`
(Optional) This should be the checksum of the entire contents of |

### upload_from_string

```
upload_from_string(
data,
content_type="text/plain",
client=None,
predefined_acl=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
checksum="auto",
retry=google.api_core.retry.retry_unary.Retry,
crc32c_checksum_value=None,
)
```


Upload contents of this blob from the provided string.

See the[and](https://cloud.google.com/storage/docs/object-versioning)

`object versioning`

[API documents for details.](https://cloud.google.com/storage/docs/lifecycle)

`lifecycle`

If `user_project`

is set on the bucket, bills the API request
to that project.

Parameters |
|
|---|---|
Name |
Description |
`data` |
`bytes or str`
The data to store in this blob. If the value is text, it will be encoded as UTF-8. |
`content_type` |
`str`
(Optional) Type of content being uploaded. Defaults to |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`predefined_acl` |
`str`
(Optional) Predefined access control list |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. If the upload is completed in a single request, the checksum will be entirely precomputed and the remote server will handle verification and error handling. If the upload is too large and must be transmitted in multiple requests, the checksum will be incrementally computed and the client will handle verification and error handling, raising |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`crc32c_checksum_value` |
`str`
(Optional) This should be the checksum of the entire contents of |