---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/summary_property.html
fetched_at: 2026-01-25T12:08:36.580448
---

# Package Properties and Attributes (3.7.0)

Summary of entries of Properties and Attributes for storage.

### google.cloud.storage.acl.ACL.PREDEFINED_JSON_ACLS

### google.cloud.storage.acl.ACL.client

Abstract getter for the object client.

See more: [google.cloud.storage.acl.ACL.client](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_client)

### google.cloud.storage.acl.BucketACL.client

The client bound to this ACL's bucket.

### google.cloud.storage.acl.BucketACL.reload_path

Compute the path for GET API requests for this ACL.

### google.cloud.storage.acl.BucketACL.save_path

Compute the path for PATCH API requests for this ACL.

### google.cloud.storage.acl.BucketACL.user_project

Compute the user project charged for API requests for this ACL.

### google.cloud.storage.acl.ObjectACL.client

The client bound to this ACL's blob.

### google.cloud.storage.acl.ObjectACL.reload_path

Compute the path for GET API requests for this ACL.

### google.cloud.storage.acl.ObjectACL.save_path

Compute the path for PATCH API requests for this ACL.

### google.cloud.storage.acl.ObjectACL.user_project

Compute the user project charged for API requests for this ACL.

### google.cloud.storage.blob.Blob.STORAGE_CLASSES

Allowed values for `storage_class`

.

### google.cloud.storage.blob.Blob.acl

Create our ACL on demand.

See more: [google.cloud.storage.blob.Blob.acl](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_acl)

### google.cloud.storage.blob.Blob.bucket

Bucket which contains the object.

See more: [google.cloud.storage.blob.Blob.bucket](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_bucket)

### google.cloud.storage.blob.Blob.cache_control

Scalar property getter.

### google.cloud.storage.blob.Blob.chunk_size

Get the blob's default chunk size.

### google.cloud.storage.blob.Blob.client

The client bound to this blob.

See more: [google.cloud.storage.blob.Blob.client](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_client)

### google.cloud.storage.blob.Blob.component_count

Number of underlying components that make up this object.

### google.cloud.storage.blob.Blob.content_disposition

Scalar property getter.

See more: [google.cloud.storage.blob.Blob.content_disposition](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_content_disposition)

### google.cloud.storage.blob.Blob.content_encoding

Scalar property getter.

### google.cloud.storage.blob.Blob.content_language

Scalar property getter.

### google.cloud.storage.blob.Blob.content_type

Scalar property getter.

### google.cloud.storage.blob.Blob.crc32c

Scalar property getter.

See more: [google.cloud.storage.blob.Blob.crc32c](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_crc32c)

### google.cloud.storage.blob.Blob.custom_time

Retrieve the custom time for the object.

### google.cloud.storage.blob.Blob.encryption_key

Retrieve the customer-supplied encryption key for the object.

### google.cloud.storage.blob.Blob.etag

Retrieve the ETag for the object.

See more: [google.cloud.storage.blob.Blob.etag](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_etag)

### google.cloud.storage.blob.Blob.event_based_hold

Scalar property getter.

### google.cloud.storage.blob.Blob.generation

Retrieve the generation for the object.

### google.cloud.storage.blob.Blob.hard_delete_time

If this object has been soft-deleted, returns the time at which it will be permanently deleted.

### google.cloud.storage.blob.Blob.id

Retrieve the ID for the object.

See more: [google.cloud.storage.blob.Blob.id](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_id)

### google.cloud.storage.blob.Blob.kms_key_name

Resource name of Cloud KMS key used to encrypt the blob's contents.

### google.cloud.storage.blob.Blob.md5_hash

Scalar property getter.

See more: [google.cloud.storage.blob.Blob.md5_hash](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_md5_hash)

### google.cloud.storage.blob.Blob.media_link

Retrieve the media download URI for the object.

### google.cloud.storage.blob.Blob.metadata

Retrieve arbitrary/application specific metadata for the object.

See more: [google.cloud.storage.blob.Blob.metadata](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_metadata)

### google.cloud.storage.blob.Blob.metageneration

Retrieve the metageneration for the object.

### google.cloud.storage.blob.Blob.owner

Retrieve info about the owner of the object.

See more: [google.cloud.storage.blob.Blob.owner](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_owner)

### google.cloud.storage.blob.Blob.path

Getter property for the URL path to this Blob.

See more: [google.cloud.storage.blob.Blob.path](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_path)

### google.cloud.storage.blob.Blob.public_url

The public URL for this blob.

### google.cloud.storage.blob.Blob.retention

Retrieve the retention configuration for this object.

See more: [google.cloud.storage.blob.Blob.retention](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_retention)

### google.cloud.storage.blob.Blob.retention_expiration_time

Retrieve timestamp at which the object's retention period expires.

See more: [google.cloud.storage.blob.Blob.retention_expiration_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_retention_expiration_time)

### google.cloud.storage.blob.Blob.self_link

Retrieve the URI for the object.

See more: [google.cloud.storage.blob.Blob.self_link](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_self_link)

### google.cloud.storage.blob.Blob.size

Size of the object, in bytes.

See more: [google.cloud.storage.blob.Blob.size](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_size)

### google.cloud.storage.blob.Blob.soft_delete_time

If this object has been soft-deleted, returns the time at which it became soft-deleted.

### google.cloud.storage.blob.Blob.storage_class

Scalar property getter.

### google.cloud.storage.blob.Blob.temporary_hold

Scalar property getter.

### google.cloud.storage.blob.Blob.time_created

Retrieve the timestamp at which the object was created.

### google.cloud.storage.blob.Blob.time_deleted

Retrieve the timestamp at which the object was deleted.

### google.cloud.storage.blob.Blob.updated

Retrieve the timestamp at which the object was updated.

See more: [google.cloud.storage.blob.Blob.updated](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_updated)

### google.cloud.storage.blob.Blob.user_project

Project ID billed for API requests made via this blob.

### google.cloud.storage.blob.Retention.blob

Blob for which this retention configuration applies to.

See more: [google.cloud.storage.blob.Retention.blob](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_blob)

### google.cloud.storage.blob.Retention.mode

The mode of the retention configuration.

See more: [google.cloud.storage.blob.Retention.mode](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_mode)

### google.cloud.storage.blob.Retention.retain_until_time

The earliest time that the object can be deleted or replaced, which is the retention configuration set for this object.

See more: [google.cloud.storage.blob.Retention.retain_until_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_retain_until_time)

### google.cloud.storage.blob.Retention.retention_expiration_time

The earliest time that the object can be deleted, which depends on any retention configuration set for the object and any retention policy set for the bucket that contains the object.

See more: [google.cloud.storage.blob.Retention.retention_expiration_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_retention_expiration_time)

### google.cloud.storage.bucket.Bucket.STORAGE_CLASSES

Allowed values for `storage_class`

.

See more: [google.cloud.storage.bucket.Bucket.STORAGE_CLASSES](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_STORAGE_CLASSES)

### google.cloud.storage.bucket.Bucket.acl

Create our ACL on demand.

See more: [google.cloud.storage.bucket.Bucket.acl](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_acl)

### google.cloud.storage.bucket.Bucket.autoclass_enabled

Whether Autoclass is enabled for this bucket.

See more: [google.cloud.storage.bucket.Bucket.autoclass_enabled](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_autoclass_enabled)

### google.cloud.storage.bucket.Bucket.autoclass_terminal_storage_class

The storage class that objects in an Autoclass bucket eventually transition to if they are not read for a certain length of time.

See more: [google.cloud.storage.bucket.Bucket.autoclass_terminal_storage_class](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_autoclass_terminal_storage_class)

### google.cloud.storage.bucket.Bucket.autoclass_terminal_storage_class_update_time

The time at which the Autoclass terminal_storage_class field was last updated for this bucket.

See more: [google.cloud.storage.bucket.Bucket.autoclass_terminal_storage_class_update_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_autoclass_terminal_storage_class_update_time)

### google.cloud.storage.bucket.Bucket.autoclass_toggle_time

Retrieve the toggle time when Autoclaass was last enabled or disabled for the bucket.

See more: [google.cloud.storage.bucket.Bucket.autoclass_toggle_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_autoclass_toggle_time)

### google.cloud.storage.bucket.Bucket.client

The client bound to this bucket.

### google.cloud.storage.bucket.Bucket.cors

Retrieve or set CORS policies configured for this bucket.

See more: [google.cloud.storage.bucket.Bucket.cors](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_cors)

### google.cloud.storage.bucket.Bucket.data_locations

Retrieve the list of regional locations for custom dual-region buckets.

### google.cloud.storage.bucket.Bucket.default_event_based_hold

Scalar property getter.

See more: [google.cloud.storage.bucket.Bucket.default_event_based_hold](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_default_event_based_hold)

### google.cloud.storage.bucket.Bucket.default_kms_key_name

Retrieve / set default KMS encryption key for objects in the bucket.

See more: [google.cloud.storage.bucket.Bucket.default_kms_key_name](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_default_kms_key_name)

### google.cloud.storage.bucket.Bucket.default_object_acl

Create our defaultObjectACL on demand.

See more: [google.cloud.storage.bucket.Bucket.default_object_acl](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_default_object_acl)

### google.cloud.storage.bucket.Bucket.etag

Retrieve the ETag for the bucket.

See more: [google.cloud.storage.bucket.Bucket.etag](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_etag)

### google.cloud.storage.bucket.Bucket.generation

Retrieve the generation for the bucket.

### google.cloud.storage.bucket.Bucket.hard_delete_time

If this bucket has been soft-deleted, returns the time at which it will be permanently deleted.

See more: [google.cloud.storage.bucket.Bucket.hard_delete_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_hard_delete_time)

### google.cloud.storage.bucket.Bucket.hierarchical_namespace_enabled

Whether hierarchical namespace is enabled for this bucket.

See more: [google.cloud.storage.bucket.Bucket.hierarchical_namespace_enabled](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_hierarchical_namespace_enabled)

### google.cloud.storage.bucket.Bucket.iam_configuration

Retrieve IAM configuration for this bucket.

See more: [google.cloud.storage.bucket.Bucket.iam_configuration](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_iam_configuration)

### google.cloud.storage.bucket.Bucket.id

Retrieve the ID for the bucket.

See more: [google.cloud.storage.bucket.Bucket.id](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_id)

### google.cloud.storage.bucket.Bucket.ip_filter

Retrieve or set the IP Filter configuration for this bucket.

### google.cloud.storage.bucket.Bucket.labels

Retrieve or set labels assigned to this bucket.

### google.cloud.storage.bucket.Bucket.lifecycle_rules

Retrieve or set lifecycle rules configured for this bucket.

See more: [google.cloud.storage.bucket.Bucket.lifecycle_rules](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_lifecycle_rules)

### google.cloud.storage.bucket.Bucket.location

Retrieve location configured for this bucket.

### google.cloud.storage.bucket.Bucket.location_type

Retrieve the location type for the bucket.

### google.cloud.storage.bucket.Bucket.metageneration

Retrieve the metageneration for the bucket.

### google.cloud.storage.bucket.Bucket.object_retention_mode

Retrieve the object retention mode set on the bucket.

See more: [google.cloud.storage.bucket.Bucket.object_retention_mode](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_object_retention_mode)

### google.cloud.storage.bucket.Bucket.owner

Retrieve info about the owner of the bucket.

See more: [google.cloud.storage.bucket.Bucket.owner](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_owner)

### google.cloud.storage.bucket.Bucket.path

The URL path to this bucket.

See more: [google.cloud.storage.bucket.Bucket.path](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_path)

### google.cloud.storage.bucket.Bucket.project_number

Retrieve the number of the project to which the bucket is assigned.

### google.cloud.storage.bucket.Bucket.requester_pays

Does the requester pay for API requests for this bucket?.

### google.cloud.storage.bucket.Bucket.retention_period

Retrieve or set the retention period for items in the bucket.

See more: [google.cloud.storage.bucket.Bucket.retention_period](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_retention_period)

### google.cloud.storage.bucket.Bucket.retention_policy_effective_time

Retrieve the effective time of the bucket's retention policy.

See more: [google.cloud.storage.bucket.Bucket.retention_policy_effective_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_retention_policy_effective_time)

### google.cloud.storage.bucket.Bucket.retention_policy_locked

Retrieve whthere the bucket's retention policy is locked.

See more: [google.cloud.storage.bucket.Bucket.retention_policy_locked](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_retention_policy_locked)

### google.cloud.storage.bucket.Bucket.rpo

Get the RPO (Recovery Point Objective) of this bucket.

See more: [google.cloud.storage.bucket.Bucket.rpo](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_rpo)

### google.cloud.storage.bucket.Bucket.self_link

Retrieve the URI for the bucket.

### google.cloud.storage.bucket.Bucket.soft_delete_policy

Retrieve the soft delete policy for this bucket.

See more: [google.cloud.storage.bucket.Bucket.soft_delete_policy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_soft_delete_policy)

### google.cloud.storage.bucket.Bucket.soft_delete_time

If this bucket has been soft-deleted, returns the time at which it became soft-deleted.

See more: [google.cloud.storage.bucket.Bucket.soft_delete_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_soft_delete_time)

### google.cloud.storage.bucket.Bucket.storage_class

Retrieve or set the storage class for the bucket.

### google.cloud.storage.bucket.Bucket.time_created

Retrieve the timestamp at which the bucket was created.

### google.cloud.storage.bucket.Bucket.updated

Retrieve the timestamp at which the bucket was last updated.

### google.cloud.storage.bucket.Bucket.user_project

Project ID to be billed for API requests made via this bucket.

### google.cloud.storage.bucket.Bucket.versioning_enabled

Is versioning enabled for this bucket?.

See more: [google.cloud.storage.bucket.Bucket.versioning_enabled](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_versioning_enabled)

### google.cloud.storage.bucket.IAMConfiguration.bucket

Bucket for which this instance is the policy.

See more: [google.cloud.storage.bucket.IAMConfiguration.bucket](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_bucket)

### google.cloud.storage.bucket.IAMConfiguration.bucket_policy_only_enabled

Deprecated alias for `uniform_bucket_level_access_enabled`

.

See more: [google.cloud.storage.bucket.IAMConfiguration.bucket_policy_only_enabled](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_bucket_policy_only_enabled)

### google.cloud.storage.bucket.IAMConfiguration.bucket_policy_only_locked_time

Deprecated alias for `uniform_bucket_level_access_locked_time`

.

See more: [google.cloud.storage.bucket.IAMConfiguration.bucket_policy_only_locked_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_bucket_policy_only_locked_time)

### google.cloud.storage.bucket.IAMConfiguration.public_access_prevention

Setting for public access prevention policy.

See more: [google.cloud.storage.bucket.IAMConfiguration.public_access_prevention](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_public_access_prevention)

### google.cloud.storage.bucket.IAMConfiguration.uniform_bucket_level_access_enabled

If set, access checks only use bucket-level IAM policies or above.

See more: [google.cloud.storage.bucket.IAMConfiguration.uniform_bucket_level_access_enabled](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_uniform_bucket_level_access_enabled)

### google.cloud.storage.bucket.IAMConfiguration.uniform_bucket_level_access_locked_time

Deadline for changing `uniform_bucket_level_access_enabled`

from true to false.

See more: [google.cloud.storage.bucket.IAMConfiguration.uniform_bucket_level_access_locked_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_uniform_bucket_level_access_locked_time)

### google.cloud.storage.bucket.LifecycleRuleConditions.age

Conditon's age value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.age](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_age)

### google.cloud.storage.bucket.LifecycleRuleConditions.created_before

Conditon's created_before value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.created_before](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_created_before)

### google.cloud.storage.bucket.LifecycleRuleConditions.custom_time_before

Conditon's 'custom_time_before' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.custom_time_before](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_custom_time_before)

### google.cloud.storage.bucket.LifecycleRuleConditions.days_since_custom_time

Conditon's 'days_since_custom_time' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.days_since_custom_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_days_since_custom_time)

### google.cloud.storage.bucket.LifecycleRuleConditions.days_since_noncurrent_time

Conditon's 'days_since_noncurrent_time' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.days_since_noncurrent_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_days_since_noncurrent_time)

### google.cloud.storage.bucket.LifecycleRuleConditions.is_live

Conditon's 'is_live' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.is_live](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_is_live)

### google.cloud.storage.bucket.LifecycleRuleConditions.matches_prefix

Conditon's 'matches_prefix' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.matches_prefix](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_matches_prefix)

### google.cloud.storage.bucket.LifecycleRuleConditions.matches_storage_class

Conditon's 'matches_storage_class' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.matches_storage_class](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_matches_storage_class)

### google.cloud.storage.bucket.LifecycleRuleConditions.matches_suffix

Conditon's 'matches_suffix' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.matches_suffix](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_matches_suffix)

### google.cloud.storage.bucket.LifecycleRuleConditions.noncurrent_time_before

Conditon's 'noncurrent_time_before' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.noncurrent_time_before](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_noncurrent_time_before)

### google.cloud.storage.bucket.LifecycleRuleConditions.number_of_newer_versions

Conditon's 'number_of_newer_versions' value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.number_of_newer_versions](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_number_of_newer_versions)

### google.cloud.storage.bucket.SoftDeletePolicy.bucket

Bucket for which this instance is the policy.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.bucket](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_bucket)

### google.cloud.storage.bucket.SoftDeletePolicy.effective_time

Get the effective time of the bucket's soft delete policy.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.effective_time](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_effective_time)

### google.cloud.storage.bucket.SoftDeletePolicy.retention_duration_seconds

Get the retention duration of the bucket's soft delete policy.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.retention_duration_seconds](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_retention_duration_seconds)

### google.cloud.storage.client.Client.SCOPE

The scopes required for authenticating as a Cloud Storage consumer.

See more: [google.cloud.storage.client.Client.SCOPE](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_SCOPE)

### google.cloud.storage.client.Client.current_batch

Currently-active batch.

### google.cloud.storage.exceptions.DataCorruption.response

The HTTP response object that caused the failure.

See more: [google.cloud.storage.exceptions.DataCorruption.response](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.exceptions.DataCorruption#google_cloud_storage_exceptions_DataCorruption_response)

### google.cloud.storage.exceptions.InvalidResponse.response

The HTTP response object that caused the failure.

See more: [google.cloud.storage.exceptions.InvalidResponse.response](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.exceptions.InvalidResponse#google_cloud_storage_exceptions_InvalidResponse_response)

### google.cloud.storage.hmac_key.HMACKeyMetadata.ACTIVE_STATE

Key is active, and may be used to sign requests.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.ACTIVE_STATE](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_ACTIVE_STATE)

### google.cloud.storage.hmac_key.HMACKeyMetadata.DELETED_STATE

Key is deleted.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.DELETED_STATE](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_DELETED_STATE)

### google.cloud.storage.hmac_key.HMACKeyMetadata.INACTIVE_STATE

Key is inactive, and may not be used to sign requests.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.INACTIVE_STATE](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_INACTIVE_STATE)

### google.cloud.storage.hmac_key.HMACKeyMetadata.access_id

Access ID of the key.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.access_id](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_access_id)

### google.cloud.storage.hmac_key.HMACKeyMetadata.etag

ETag identifying the version of the key metadata.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.etag](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_etag)

### google.cloud.storage.hmac_key.HMACKeyMetadata.id

ID of the key, including the Project ID and the Access ID.

### google.cloud.storage.hmac_key.HMACKeyMetadata.path

Resource path for the metadata's key.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.path](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_path)

### google.cloud.storage.hmac_key.HMACKeyMetadata.project

Project ID associated with the key.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.project](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_project)

### google.cloud.storage.hmac_key.HMACKeyMetadata.service_account_email

Service account e-mail address associated with the key.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.service_account_email](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_service_account_email)

### google.cloud.storage.hmac_key.HMACKeyMetadata.state

Get / set key's state.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.state](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_state)

### google.cloud.storage.hmac_key.HMACKeyMetadata.time_created

Retrieve the timestamp at which the HMAC key was created.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.time_created](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_time_created)

### google.cloud.storage.hmac_key.HMACKeyMetadata.updated

Retrieve the timestamp at which the HMAC key was created.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.updated](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_updated)

### google.cloud.storage.hmac_key.HMACKeyMetadata.user_project

Project ID to be billed for API requests made via this bucket.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.user_project](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_user_project)

### google.cloud.storage.notification.BucketNotification.blob_name_prefix

Prefix of blob names for which notification events are published.

See more: [google.cloud.storage.notification.BucketNotification.blob_name_prefix](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_blob_name_prefix)

### google.cloud.storage.notification.BucketNotification.bucket

Bucket to which the notification is bound.

See more: [google.cloud.storage.notification.BucketNotification.bucket](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_bucket)

### google.cloud.storage.notification.BucketNotification.client

The client bound to this notfication.

See more: [google.cloud.storage.notification.BucketNotification.client](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_client)

### google.cloud.storage.notification.BucketNotification.custom_attributes

Custom attributes passed with notification events.

See more: [google.cloud.storage.notification.BucketNotification.custom_attributes](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_custom_attributes)

### google.cloud.storage.notification.BucketNotification.etag

Server-set ETag of notification resource.

See more: [google.cloud.storage.notification.BucketNotification.etag](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_etag)

### google.cloud.storage.notification.BucketNotification.event_types

Event types for which notification events are published.

See more: [google.cloud.storage.notification.BucketNotification.event_types](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_event_types)

### google.cloud.storage.notification.BucketNotification.notification_id

Server-set ID of notification resource.

See more: [google.cloud.storage.notification.BucketNotification.notification_id](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_notification_id)

### google.cloud.storage.notification.BucketNotification.path

The URL path for this notification.

See more: [google.cloud.storage.notification.BucketNotification.path](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_path)

### google.cloud.storage.notification.BucketNotification.payload_format

Format of payload of notification events.

See more: [google.cloud.storage.notification.BucketNotification.payload_format](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_payload_format)

### google.cloud.storage.notification.BucketNotification.self_link

Server-set ETag of notification resource.

See more: [google.cloud.storage.notification.BucketNotification.self_link](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_self_link)

### google.cloud.storage.notification.BucketNotification.topic_name

Topic name to which notifications are published.

See more: [google.cloud.storage.notification.BucketNotification.topic_name](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_topic_name)

### google.cloud.storage.notification.BucketNotification.topic_project

Project ID of topic to which notifications are published.

See more: [google.cloud.storage.notification.BucketNotification.topic_project](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_topic_project)