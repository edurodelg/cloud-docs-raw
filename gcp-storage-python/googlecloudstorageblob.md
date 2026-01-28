---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob
fetched_at: 2026-01-28T07:25:19.306063
---

# Module blob (3.7.0)

Create / interact with Google Cloud Storage blobs.

## Classes

[Blob](/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob)

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

Parameters |
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

[Retention](/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention)

`Retention(blob, mode=None, retain_until_time=None, retention_expiration_time=None)`


Map an object's retention configuration.