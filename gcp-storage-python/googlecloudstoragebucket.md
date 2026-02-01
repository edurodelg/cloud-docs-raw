---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket
fetched_at: 2026-02-01T07:57:52.054748
---

# Module bucket (3.8.0)

Create / interact with Google Cloud Storage buckets.

## Classes

[Bucket](/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket)

`Bucket(client, name=None, user_project=None, generation=None)`


A class representing a Bucket on Cloud Storage.

Parameters |
|
|---|---|
Name |
Description |
`client` |
A client which holds credentials and project configuration for the bucket (which requires a project). |
`name` |
`str`
The name of the bucket. Bucket names must start and end with a number or letter. |
`user_project` |
`str`
(Optional) the project ID to be billed for API requests made via this instance. |
`generation` |
`int`
(Optional) If present, selects a specific revision of this bucket. |

[IAMConfiguration](/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration)

```
IAMConfiguration(
bucket,
public_access_prevention=object,
uniform_bucket_level_access_enabled=object,
uniform_bucket_level_access_locked_time=object,
bucket_policy_only_enabled=object,
bucket_policy_only_locked_time=object,
)
```


Map a bucket's IAM configuration.

[LifecycleRuleAbortIncompleteMultipartUpload](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload)

`LifecycleRuleAbortIncompleteMultipartUpload(**kw)`


Map a rule aborting incomplete multipart uploads of matching items.

The "age" lifecycle condition is the only supported condition for this rule.

[LifecycleRuleConditions](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions)

```
LifecycleRuleConditions(
age=None,
created_before=None,
is_live=None,
matches_storage_class=None,
number_of_newer_versions=None,
days_since_custom_time=None,
custom_time_before=None,
days_since_noncurrent_time=None,
noncurrent_time_before=None,
matches_prefix=None,
matches_suffix=None,
_factory=False,
)
```


Map a single lifecycle rule for a bucket.

Parameters |
|
|---|---|
Name |
Description |
`age` |
`int`
(Optional) Apply rule action to items whose age, in days, exceeds this value. |
`created_before` |
`datetime.date`
(Optional) Apply rule action to items created before this date. |
`is_live` |
`bool`
(Optional) If true, apply rule action to non-versioned items, or to items with no newer versions. If false, apply rule action to versioned items with at least one newer version. |
`matches_prefix` |
`list(str)`
(Optional) Apply rule action to items which any prefix matches the beginning of the item name. |
`matches_storage_class` |
`list(str), one or more of `
(Optional) Apply rule action to items whose storage class matches this value. |
`matches_suffix` |
`list(str)`
(Optional) Apply rule action to items which any suffix matches the end of the item name. |
`number_of_newer_versions` |
`int`
(Optional) Apply rule action to versioned items having N newer versions. |
`days_since_custom_time` |
`int`
(Optional) Apply rule action to items whose number of days elapsed since the custom timestamp. This condition is relevant only for versioned objects. The value of the field must be a non negative integer. If it's zero, the object version will become eligible for lifecycle action as soon as it becomes custom. |
`custom_time_before` |
(Optional) Date object parsed from RFC3339 valid date, apply rule action to items whose custom time is before this date. This condition is relevant only for versioned objects, e.g., 2019-03-16. |
`days_since_noncurrent_time` |
`int`
(Optional) Apply rule action to items whose number of days elapsed since the non current timestamp. This condition is relevant only for versioned objects. The value of the field must be a non negative integer. If it's zero, the object version will become eligible for lifecycle action as soon as it becomes non current. |
`noncurrent_time_before` |
(Optional) Date object parsed from RFC3339 valid date, apply rule action to items whose non current time is before this date. This condition is relevant only for versioned objects, e.g, 2019-03-16. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if no arguments are passed. |

[LifecycleRuleDelete](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete)

`LifecycleRuleDelete(**kw)`


Map a lifecycle rule deleting matching items.

[LifecycleRuleSetStorageClass](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass)

`LifecycleRuleSetStorageClass(storage_class, **kw)`


Map a lifecycle rule updating storage class of matching items.

Parameter |
|
|---|---|
Name |
Description |
`storage_class` |
`str, one of `
new storage class to assign to matching items. |

[SoftDeletePolicy](/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy)

`SoftDeletePolicy(bucket, **kw)`


Map a bucket's soft delete policy.

Parameters |
|
|---|---|
Name |
Description |
`bucket` |
Bucket for which this instance is the policy. |
`retention_duration_seconds` |
`int`
(Optional) The period of time in seconds that soft-deleted objects in the bucket will be retained and cannot be permanently deleted. |
`effective_time` |
(Optional) When the bucket's soft delete policy is effective. This value should normally only be set by the back-end API. |