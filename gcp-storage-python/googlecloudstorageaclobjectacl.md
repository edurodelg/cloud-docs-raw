---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ObjectACL
fetched_at: 2026-01-30T23:52:55.067585
---

# Class ObjectACL (3.8.0)

`ObjectACL(blob)`


An ACL specifically for a Cloud Storage object / blob.

## Parameter |
|
|---|---|
Name |
Description |
`blob` |
The blob that this ACL corresponds to. |

## Properties

### client

The client bound to this ACL's blob.

### reload_path

Compute the path for GET API requests for this ACL.

### save_path

Compute the path for PATCH API requests for this ACL.

### user_project

Compute the user project charged for API requests for this ACL.

## Methods

### clear

```
clear(
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Remove all ACL entries.

If `user_project`

is set, bills the API request to that project.

Note that this won't actually remove *ALL* the rules, but it
will remove all the non-default rules. In short, you'll still
have access to a bucket that you created even after you clear
ACL rules with this method.

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
(Optional) How to retry the RPC. See: |

### save

```
save(
acl=None,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Save this ACL for the current object.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`acl` |
The ACL object to save. If left blank, this will save current entries. |
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
(Optional) How to retry the RPC. See: |

### save_predefined

```
save_predefined(
predefined,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Save this ACL for the current object using a predefined ACL.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`predefined` |
`str`
An identifier for a predefined ACL. Must be one of the keys in |
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
(Optional) How to retry the RPC. See: |