---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl
fetched_at: 2026-02-06T16:56:06.674909
---

# Module acl (3.8.0)

Manage access to objects and buckets.

## Classes

[ACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL)

`ACL()`


Container class representing a list of access controls.

[BucketACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.BucketACL)

`BucketACL(bucket)`


An ACL specifically for a bucket.

Parameter |
|
|---|---|
Name |
Description |
`bucket` |
The bucket to which this ACL relates. |

[DefaultObjectACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.DefaultObjectACL)

`DefaultObjectACL(bucket)`


A class representing the default object ACL for a bucket.

[ObjectACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.ObjectACL)

`ObjectACL(blob)`


An ACL specifically for a Cloud Storage object / blob.

Parameter |
|
|---|---|
Name |
Description |
`blob` |
The blob that this ACL corresponds to. |