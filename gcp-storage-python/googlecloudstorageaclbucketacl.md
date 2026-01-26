---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.BucketACL
fetched_at: 2026-01-26T23:14:03.785648
---

# Class BucketACL (3.7.0)

`BucketACL(bucket)`


An ACL specifically for a bucket.

## Parameter |
|
|---|---|
Name |
Description |
`bucket` |
The bucket to which this ACL relates. |

## Properties

### client

The client bound to this ACL's bucket.

### reload_path

Compute the path for GET API requests for this ACL.

### save_path

Compute the path for PATCH API requests for this ACL.

### user_project

Compute the user project charged for API requests for this ACL.