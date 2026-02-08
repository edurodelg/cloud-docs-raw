---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/generation_metageneration
fetched_at: 2026-02-08T01:07:35.588489
---

# Conditional Requests Via ETag / Generation / Metageneration Preconditions

Preconditions tell Cloud Storage to only perform a request if the ETag, generation, or metageneration number of the affected object meets your precondition criteria. These checks of the ETag, generation, and metageneration numbers ensure that the object is in the expected state, allowing you to perform safe read-modify-write updates and conditional operations on objects

## Concepts

### ETag

An ETag is returned as part of the response header whenever a resource is
returned, as well as included in the resource itself. Users should make no
assumptions about the value used in an ETag except that it changes whenever the
underlying data changes, per the
[specification](https://tools.ietf.org/html/rfc7232#section-2.3)

The `ETag`

attribute is set by the GCS back-end, and is read-only in the
client library.

### Metageneration

When you create a [ Bucket](/python/docs/reference/storage/latest/storage/bucket#google.cloud.storage.bucket.Bucket),
its

[is initialized to](/python/docs/reference/storage/latest/storage/bucket#google.cloud.storage.bucket.Bucket.metageneration)

`metageneration`

`1`

, representing the initial version of the bucket’s metadata.When you first upload a
[ Blob](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob) (“Object” in the GCS back-end docs),
its

[is likewise initialized to](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.metageneration)

`metageneration`

`1`

. representing the initial version of the blob’s metadata.The `metageneration`

attribute is set by the GCS back-end, and is read-only
in the client library.

Each time you patch or update the bucket’s / blob’s metadata, its
`metageneration`

is incremented.

### Generation

Each time you upload a new version of a file to a
[ Blob](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob) (“Object” in the GCS back-end docs),
the Blob’s

`generation`

is changed, and its
`metageneration`

is reset to `1`

(the first
metadata version for that generation of the blob).The `generation`

attribute is set by the GCS back-end, and is read-only
in the client library.

### See also

## Conditional Parameters

### Using `if_etag_match`


Passing the `if_etag_match`

parameter to a method which retrieves a
blob resource (e.g.,
[ Blob.reload](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.reload))
makes the operation conditional on whether the blob’s current

`ETag`

matches
the given value. This parameter is not supported for modification (e.g.,
[).](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.update)

`Blob.update`

### Using `if_etag_not_match`


Passing the `if_etag_not_match`

parameter to a method which retrieves a
blob resource (e.g.,
[ Blob.reload](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.reload))
makes the operation conditional on whether the blob’s current

`ETag`

matches
the given value. This parameter is not supported for modification (e.g.,
[).](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.update)

`Blob.update`

### Using `if_generation_match`


Passing the `if_generation_match`

parameter to a method which retrieves a
blob resource (e.g.,
[ Blob.reload](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.reload)) or modifies
the blob (e.g.,

[) makes the operation conditional on whether the blob’s current](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.update)

`Blob.update`

`generation`

matches the given value.As a special case, passing `0`

as the value for `if_generation_match`

makes the operation succeed only if there are no live versions of the blob.

### Using `if_generation_not_match`


Passing the `if_generation_not_match`

parameter to a method which retrieves
a blob resource (e.g.,
[ Blob.reload](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.reload)) or modifies
the blob (e.g.,

[) makes the operation conditional on whether the blob’s current](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.update)

`Blob.update`

`generation`

does **not**match the given value.

If no live version of the blob exists, the precondition fails.

As a special case, passing `0`

as the value for `if_generation_not_match`

makes the operation succeed only if there **is** a live version of the blob.

### Using `if_metageneration_match`


Passing the `if_metageneration_match`

parameter to a method which retrieves
a blob or bucket resource
(e.g., [ Blob.reload](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.reload),

[) or modifies the blob or bucket (e.g.,](/python/docs/reference/storage/latest/storage/bucket#google.cloud.storage.bucket.Bucket.reload)

`Bucket.reload`


`Blob.update`

[) makes the operation conditional on whether the resource’s current](/python/docs/reference/storage/latest/storage/bucket#google.cloud.storage.bucket.Bucket.patch)

`Bucket.patch`

`metageneration`

matches the given value.### Using `if_metageneration_not_match`


Passing the `if_metageneration_not_match`

parameter to a method which
retrieves a blob or bucket resource
(e.g., [ Blob.reload](/python/docs/reference/storage/latest/storage/blob#google.cloud.storage.blob.Blob.reload),

[) or modifies the blob or bucket (e.g.,](/python/docs/reference/storage/latest/storage/bucket#google.cloud.storage.bucket.Bucket.reload)

`Bucket.reload`


`Blob.update`

[) makes the operation conditional on whether the resource’s current](/python/docs/reference/storage/latest/storage/bucket#google.cloud.storage.bucket.Bucket.patch)

`Bucket.patch`

`metageneration`

does **not**match the given value.