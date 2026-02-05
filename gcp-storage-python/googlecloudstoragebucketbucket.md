---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket
fetched_at: 2026-02-05T08:37:52.557849
---

# Class Bucket (3.8.0)

`Bucket(client, name=None, user_project=None, generation=None)`


A class representing a Bucket on Cloud Storage.

## Parameters |
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

## Properties

### acl

Create our ACL on demand.

### autoclass_enabled

Whether Autoclass is enabled for this bucket.

See [https://cloud.google.com/storage/docs/using-autoclass](https://cloud.google.com/storage/docs/using-autoclass) for details.

:setter: Update whether autoclass is enabled for this bucket. :getter: Query whether autoclass is enabled for this bucket.

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if enabled, else False. |

### autoclass_terminal_storage_class

The storage class that objects in an Autoclass bucket eventually transition to if they are not read for a certain length of time. Valid values are NEARLINE and ARCHIVE.

See [https://cloud.google.com/storage/docs/using-autoclass](https://cloud.google.com/storage/docs/using-autoclass) for details.

:setter: Set the terminal storage class for Autoclass configuration. :getter: Get the terminal storage class for Autoclass configuration.

Returns |
|
|---|---|
Type |
Description |
`str` |
The terminal storage class if Autoclass is enabled, else `None` . |

### autoclass_terminal_storage_class_update_time

The time at which the Autoclass terminal_storage_class field was last updated for this bucket

Returns |
|
|---|---|
Type |
Description |
`datetime.datetime or ` |
point-in time at which the bucket's terminal_storage_class is last updated, or `None` if the property is not set locally. |

### autoclass_toggle_time

Retrieve the toggle time when Autoclaass was last enabled or disabled for the bucket.

Returns |
|
|---|---|
Type |
Description |
`datetime.datetime or ` |
point-in time at which the bucket's autoclass is toggled, or `None` if the property is not set locally. |

### client

The client bound to this bucket.

### cors

Retrieve or set CORS policies configured for this bucket.

See [http://www.w3.org/TR/cors/](http://www.w3.org/TR/cors/) and
[https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`list of dictionaries` |
A sequence of mappings describing each CORS policy. |

### data_locations

Retrieve the list of regional locations for custom dual-region buckets.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets) and
[https://cloud.google.com/storage/docs/locations](https://cloud.google.com/storage/docs/locations)

Returns `None`

if the property has not been set before creation,
if the bucket's resource has not been loaded from the server,
or if the bucket is not a dual-regions bucket.

### default_event_based_hold

Scalar property getter.

### default_kms_key_name

Retrieve / set default KMS encryption key for objects in the bucket.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

:setter: Set default KMS encryption key for items in this bucket. :getter: Get default KMS encryption key for items in this bucket.

Returns |
|
|---|---|
Type |
Description |
`str` |
Default KMS encryption key, or `None` if not set. |

### default_object_acl

Create our defaultObjectACL on demand.

### etag

Retrieve the ETag for the bucket.

See [https://tools.ietf.org/html/rfc2616#section-3.11](https://tools.ietf.org/html/rfc2616#section-3.11) and
[https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The bucket etag or `None` if the bucket's resource has not been loaded from the server. |

### generation

Retrieve the generation for the bucket.

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The generation of the bucket or `None` if the bucket's resource has not been loaded from the server. |

### hard_delete_time

If this bucket has been soft-deleted, returns the time at which it will be permanently deleted.

Returns |
|
|---|---|
Type |
Description |
|
(readonly) The time that the bucket will be permanently deleted. Note this property is only set for soft-deleted buckets. |

### hierarchical_namespace_enabled

Whether hierarchical namespace is enabled for this bucket.

:setter: Update whether hierarchical namespace is enabled for this bucket. :getter: Query whether hierarchical namespace is enabled for this bucket.

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if enabled, else False. |

### iam_configuration

Retrieve IAM configuration for this bucket.

Returns |
|
|---|---|
Type |
Description |
|
an instance for managing the bucket's IAM configuration. |

### id

Retrieve the ID for the bucket.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The ID of the bucket or `None` if the bucket's resource has not been loaded from the server. |

### ip_filter

Retrieve or set the IP Filter configuration for this bucket.

See [https://cloud.google.com/storage/docs/ip-filtering-overview](https://cloud.google.com/storage/docs/ip-filtering-overview) and
[https://cloud.google.com/storage/docs/json_api/v1/buckets#ipFilter](https://cloud.google.com/storage/docs/json_api/v1/buckets#ipFilter)

```
from google.cloud.storage.ip_filter import (
IPFilter,
PublicNetworkSource,
)
ip_filter = IPFilter()
ip_filter.mode = "Enabled"
ip_filter.public_network_source = PublicNetworkSource(
allowed_ip_cidr_ranges=["203.0.113.5/32"]
)
bucket.ip_filter = ip_filter
bucket.patch()
```


:setter: Set the IP Filter configuration for this bucket. :getter: Gets the IP Filter configuration for this bucket.

Returns |
|
|---|---|
Type |
Description |
`IPFilter or ` |
An `IPFilter` object representing the configuration, or `None` if no filter is configured. |

### labels

Retrieve or set labels assigned to this bucket.

See
[https://cloud.google.com/storage/docs/json_api/v1/buckets#labels](https://cloud.google.com/storage/docs/json_api/v1/buckets#labels)

Returns |
|
|---|---|
Type |
Description |
|
Name-value pairs (string->string) labelling the bucket. |

### lifecycle_rules

Retrieve or set lifecycle rules configured for this bucket.

See [https://cloud.google.com/storage/docs/lifecycle](https://cloud.google.com/storage/docs/lifecycle) and
[https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`generator(dict)` |
A sequence of mappings describing each lifecycle rule. |

### location

Retrieve location configured for this bucket.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets) and
[https://cloud.google.com/storage/docs/locations](https://cloud.google.com/storage/docs/locations)

Returns `None`

if the property has not been set before creation,
or if the bucket's resource has not been loaded from the server.

### location_type

Retrieve the location type for the bucket.

See [https://cloud.google.com/storage/docs/storage-classes](https://cloud.google.com/storage/docs/storage-classes)

:getter: Gets the the location type for this bucket.

Returns |
|
|---|---|
Type |
Description |
`str or ` |
If set, one of MULTI_REGION_LOCATION_TYPE, REGION_LOCATION_TYPE, or DUAL_REGION_LOCATION_TYPE, else `None` . |

### metageneration

Retrieve the metageneration for the bucket.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The metageneration of the bucket or `None` if the bucket's resource has not been loaded from the server. |

### object_retention_mode

Retrieve the object retention mode set on the bucket.

Returns |
|
|---|---|
Type |
Description |
`str` |
When set to Enabled, retention configurations can be set on objects in the bucket. |

### owner

Retrieve info about the owner of the bucket.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`dict or ` |
Mapping of owner's role/ID. Returns `None` if the bucket's resource has not been loaded from the server. |

### path

The URL path to this bucket.

### project_number

Retrieve the number of the project to which the bucket is assigned.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The project number that owns the bucket or `None` if the bucket's resource has not been loaded from the server. |

### requester_pays

Does the requester pay for API requests for this bucket?

See [https://cloud.google.com/storage/docs/requester-pays](https://cloud.google.com/storage/docs/requester-pays) for
details.

:setter: Update whether requester pays for this bucket. :getter: Query whether requester pays for this bucket.

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if requester pays for API requests for the bucket, else False. |

### retention_period

Retrieve or set the retention period for items in the bucket.

Returns |
|
|---|---|
Type |
Description |
`int or ` |
number of seconds to retain items after upload or release from event-based lock, or `None` if the property is not set locally. |

### retention_policy_effective_time

Retrieve the effective time of the bucket's retention policy.

Returns |
|
|---|---|
Type |
Description |
`datetime.datetime or ` |
point-in time at which the bucket's retention policy is effective, or `None` if the property is not set locally. |

### retention_policy_locked

Retrieve whthere the bucket's retention policy is locked.

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if the bucket's policy is locked, or else False if the policy is not locked, or the property is not set locally. |

### rpo

Get the RPO (Recovery Point Objective) of this bucket

See: [https://cloud.google.com/storage/docs/managing-turbo-replication](https://cloud.google.com/storage/docs/managing-turbo-replication)

"ASYNC_TURBO" or "DEFAULT"

### self_link

Retrieve the URI for the bucket.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
`str or ` |
The self link for the bucket or `None` if the bucket's resource has not been loaded from the server. |

### soft_delete_policy

Retrieve the soft delete policy for this bucket.

Returns |
|
|---|---|
Type |
Description |
|
an instance for managing the bucket's soft delete policy. |

### soft_delete_time

If this bucket has been soft-deleted, returns the time at which it became soft-deleted.

Returns |
|
|---|---|
Type |
Description |
|
(readonly) The time that the bucket became soft-deleted. Note this property is only set for soft-deleted buckets. |

### storage_class

Retrieve or set the storage class for the bucket.

See [https://cloud.google.com/storage/docs/storage-classes](https://cloud.google.com/storage/docs/storage-classes)

:setter: Set the storage class for this bucket. :getter: Gets the the storage class for this bucket.

Returns |
|
|---|---|
Type |
Description |
`str or ` |
If set, one of NEARLINE_STORAGE_CLASS, COLDLINE_STORAGE_CLASS, ARCHIVE_STORAGE_CLASS, STANDARD_STORAGE_CLASS, MULTI_REGIONAL_LEGACY_STORAGE_CLASS, REGIONAL_LEGACY_STORAGE_CLASS, or DURABLE_REDUCED_AVAILABILITY_LEGACY_STORAGE_CLASS, else `None` . |

### time_created

Retrieve the timestamp at which the bucket was created.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the bucket's resource has not been loaded from the server. |

### updated

Retrieve the timestamp at which the bucket was last updated.

See [https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the bucket's resource has not been loaded from the server. |

### user_project

Project ID to be billed for API requests made via this bucket.

If unset, API requests are billed to the bucket owner.

A user project is required for all operations on Requester Pays buckets.

See [https://cloud.google.com/storage/docs/requester-pays#requirements](https://cloud.google.com/storage/docs/requester-pays#requirements) for details.

### versioning_enabled

Is versioning enabled for this bucket?

See [https://cloud.google.com/storage/docs/object-versioning](https://cloud.google.com/storage/docs/object-versioning) for
details.

:setter: Update whether versioning is enabled for this bucket. :getter: Query whether versioning is enabled for this bucket.

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if enabled, else False. |

## Methods

### Bucket

`Bucket(client, name=None, user_project=None, generation=None)`


property `name`

Get the bucket's name.

### add_lifecycle_abort_incomplete_multipart_upload_rule

`add_lifecycle_abort_incomplete_multipart_upload_rule(**kw)`


Add a "abort incomplete multipart upload" rule to lifecycle rules.

This defines a[lifecycle configuration](https://cloud.google.com/storage/docs/lifecycle), which is set on the bucket. For the general format of a lifecycle configuration, see the

[bucket resource representation for JSON](https://cloud.google.com/storage/docs/json_api/v1/buckets).

### add_lifecycle_delete_rule

`add_lifecycle_delete_rule(**kw)`


Add a "delete" rule to lifecycle rules configured for this bucket.

This defines a [lifecycle configuration](https://cloud.google.com/storage/docs/lifecycle),
which is set on the bucket. For the general format of a lifecycle configuration, see the
[bucket resource representation for JSON](https://cloud.google.com/storage/docs/json_api/v1/buckets).
See also a [code sample](https://cloud.google.com/storage/docs/samples/storage-enable-bucket-lifecycle-management#storage_enable_bucket_lifecycle_management-python).

### add_lifecycle_set_storage_class_rule

`add_lifecycle_set_storage_class_rule(storage_class, **kw)`


Add a "set storage class" rule to lifecycle rules.

This defines a [lifecycle configuration](https://cloud.google.com/storage/docs/lifecycle),
which is set on the bucket. For the general format of a lifecycle configuration, see the
[bucket resource representation for JSON](https://cloud.google.com/storage/docs/json_api/v1/buckets).

Parameter |
|
|---|---|
Name |
Description |
`storage_class` |
`str, one of `
new storage class to assign to matching items. |

### blob

```
blob(
blob_name, chunk_size=None, encryption_key=None, kms_key_name=None, generation=None
)
```


Factory constructor for blob object.

Parameters |
|
|---|---|
Name |
Description |
`blob_name` |
`str`
The name of the blob to be instantiated. |
`chunk_size` |
`int`
The size of a chunk of data whenever iterating (in bytes). This must be a multiple of 256 KB per the API specification. |
`encryption_key` |
`bytes`
(Optional) 32 byte encryption key for customer-supplied encryption. |
`kms_key_name` |
`str`
(Optional) Resource name of KMS key used to encrypt blob's content. |
`generation` |
`long`
(Optional) If present, selects a specific revision of this object. |
`crc32c_checksum` |
`str`
(Optional) If set, the CRC32C checksum of the blob's content. CRC32c checksum, as described in RFC 4960, Appendix B; encoded using base64 in big-endian byte order. See Apenndix B: |

Returns |
|
|---|---|
Type |
Description |
|
The blob object created. |

### clear_lifecycle_rules

`clear_lifecycle_rules()`


Clear lifecycle rules configured for this bucket.

See [https://cloud.google.com/storage/docs/lifecycle](https://cloud.google.com/storage/docs/lifecycle) and
[https://cloud.google.com/storage/docs/json_api/v1/buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

### clear_lifecyle_rules

`clear_lifecyle_rules()`


Deprecated alias for clear_lifecycle_rules.

### configure_website

`configure_website(main_page_suffix=None, not_found_page=None)`


Configure website-related properties.

Parameters |
|
|---|---|
Name |
Description |
`main_page_suffix` |
`str`
The page to use as the main page of a directory. Typically something like index.html. |
`not_found_page` |
`str`
The file to use when a page isn't found. |

### copy_blob

```
copy_blob(
blob,
destination_bucket,
new_name=None,
client=None,
preserve_acl=True,
source_generation=None,
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


Copy the given blob to the given bucket, optionally with a new name.

If `user_project`

is set, bills the API request to that project.

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/objects/copy)
and a [code sample](https://cloud.google.com/storage/docs/samples/storage-copy-file#storage_copy_file-python).

Parameters |
|
|---|---|
Name |
Description |
`blob` |
The blob to be copied. |
`destination_bucket` |
The bucket into which the blob should be copied. |
`new_name` |
`str`
(Optional) The new name for the copied file. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`preserve_acl` |
`bool`
DEPRECATED. This argument is not functional! (Optional) Copies ACL from old blob to new blob. Default: True. Note that |
`source_generation` |
`long`
(Optional) The generation of the blob to be copied. |
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
|
The new Blob. |

### create

```
create(
client=None,
project=None,
location=None,
predefined_acl=None,
predefined_default_object_acl=None,
enable_object_retention=False,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Creates current bucket.

If the bucket already exists, will raise xref_Conflict.

This implements "storage.buckets.insert".

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`project` |
`str`
(Optional) The project under which the bucket is to be created. If not passed, uses the project set on the client. |
`location` |
`str`
(Optional) The location of the bucket. If not passed, the default location, US, will be used. See |
`predefined_acl` |
`str`
(Optional) Name of predefined ACL to apply to bucket. See: |
`predefined_default_object_acl` |
`str`
(Optional) Name of predefined ACL to apply to bucket's objects. See: |
`enable_object_retention` |
`bool`
(Optional) Whether object retention should be enabled on this bucket. See: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if `project` is None and client's `project` is also None. |

### delete

```
delete(
force=False,
client=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Delete this bucket.

The bucket **must** be empty in order to submit a delete request. If
`force=True`

is passed, this will first attempt to delete all the
objects / blobs in the bucket (i.e. try to empty the bucket).

If the bucket doesn't exist, this will raise
xref_NotFound. If the bucket is not empty
(and `force=False`

), will raise xref_Conflict.

If `force=True`

and the bucket contains more than 256 objects / blobs
this will cowardly refuse to delete the objects (or the bucket). This
is to prevent accidental bucket deletion and to prevent extremely long
runtime of this method. Also note that `force=True`

is not supported
in a `Batch`

context.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`force` |
`bool`
If True, empties the bucket's objects then deletes it. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration does not match the given value. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Exceptions |
|
|---|---|
Type |
Description |
``ValueError` |
if `force` is `True` and the bucket contains more than 256 objects / blobs. |

### delete_blob

```
delete_blob(
blob_name,
client=None,
generation=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Deletes a blob from the current bucket.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`blob_name` |
`str`
A blob name to delete. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`generation` |
`long`
(Optional) If present, permanently deletes a specific revision of this object. |
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
Raises a NotFound if the blob isn't found. To suppress the exception, use `delete_blobs` by passing a no-op `on_error` callback. |

### delete_blobs

```
delete_blobs(
blobs,
on_error=None,
client=None,
preserve_generation=False,
timeout=60,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Deletes a list of blobs from the current bucket.

Uses `delete_blob`

to delete each individual blob.

By default, any generation information in the list of blobs is ignored, and the
live versions of all blobs are deleted. Set `preserve_generation`

to True
if blob generation should instead be propagated from the list of blobs.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`blobs` |
`list`
A list of |
`on_error` |
`callable`
(Optional) Takes single argument: |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`preserve_generation` |
`bool`
(Optional) Deletes only the generation specified on the blob object, instead of the live version, if set to True. Only :class: |
`if_generation_match` |
`list of long`
(Optional) See :ref: |
`if_generation_not_match` |
`list of long`
(Optional) See :ref: |
`if_metageneration_match` |
`list of long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`list of long`
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
(if `on_error` is not passed). |

### disable_logging

`disable_logging()`


Disable access logging for this bucket.

See [https://cloud.google.com/storage/docs/access-logs#disabling](https://cloud.google.com/storage/docs/access-logs#disabling)

### disable_website

`disable_website()`


Disable the website configuration for this bucket.

This is really just a shortcut for setting the website-related
attributes to `None`

.

### enable_logging

`enable_logging(bucket_name, object_prefix="")`


Enable access logging for this bucket.

Parameters |
|
|---|---|
Name |
Description |
`bucket_name` |
`str`
name of bucket in which to store access logs |
`object_prefix` |
`str`
prefix for access log filenames |

### exists

```
exists(
client=None,
timeout=60,
if_etag_match=None,
if_etag_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Determines whether or not this bucket exists.

If `user_project`

is set, bills the API request to that project.

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
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) Make the operation conditional on whether the bucket's current ETag matches the given value. |
`if_etag_not_match` |
`Union[str, Set[str]])`
(Optional) Make the operation conditional on whether the bucket's current ETag does not match the given value. |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the bucket's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the bucket's current metageneration does not match the given value. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if the bucket exists in Cloud Storage. |

### from_string

`from_string(uri, client=None)`


Get a constructor for bucket object by URI.

`from google.cloud import `[storage](https://docs.cloud.google.com/python/docs/reference/storage/latest)
from google.cloud.storage.bucket import Bucket
client = [storage](https://docs.cloud.google.com/python/docs/reference/storage/latest).[Client](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client.html)()
bucket = Bucket.[from_string](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket.html#google_cloud_storage_bucket_Bucket_from_string)("gs://bucket", client=client)


Parameters |
|
|---|---|
Name |
Description |
`uri` |
`str`
The bucket uri pass to get bucket object. |
`client` |
(Optional) The client to use. Application code should |

Returns |
|
|---|---|
Type |
Description |
|
The bucket object created. |

### from_uri

`from_uri(uri, client=None)`


Get a constructor for bucket object by URI.

`from google.cloud import `[storage](https://docs.cloud.google.com/python/docs/reference/storage/latest)
from google.cloud.storage.bucket import Bucket
client = [storage](https://docs.cloud.google.com/python/docs/reference/storage/latest).[Client](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client.html)()
bucket = Bucket.[from_uri](https://docs.cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket.html#google_cloud_storage_bucket_Bucket_from_uri)("gs://bucket", client=client)


Parameters |
|
|---|---|
Name |
Description |
`uri` |
`str`
The bucket uri pass to get bucket object. |
`client` |
(Optional) The client to use. Application code should |

Returns |
|
|---|---|
Type |
Description |
|
The bucket object created. |

### generate_signed_url

```
generate_signed_url(
expiration=None,
api_access_endpoint=None,
method="GET",
headers=None,
query_parameters=None,
client=None,
credentials=None,
version=None,
virtual_hosted_style=False,
bucket_bound_hostname=None,
scheme="http",
)
```


Generates a signed URL for this bucket.

If`bucket_bound_hostname`

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
`headers` |
`dict`
(Optional) Additional HTTP headers to be included as part of the signed URLs. See: |
`query_parameters` |
`dict`
(Optional) Additional query parameters to be included as part of the signed URLs. See: |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`credentials` |
The authorization credentials to attach to requests. These credentials identify this application to the service. If none are specified, the client will attempt to ascertain the credentials from the environment. |
`version` |
`str`
(Optional) The version of signed credential to create. Must be one of 'v2' 'v4'. |
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

### generate_upload_policy

`generate_upload_policy(conditions, expiration=None, client=None)`


Create a signed upload policy for uploading objects.

This method generates and signs a policy document. You can use
[ policy documents](https://cloud.google.com/storage/docs/xml-api/post-object-forms)
to allow visitors to a website to upload files to
Google Cloud Storage without giving them direct write access.
See a

[code sample](https://cloud.google.com/storage/docs/xml-api/post-object-forms#python).

Parameters |
|
|---|---|
Name |
Description |
`expiration` |
`datetime`
(Optional) Expiration in UTC. If not specified, the policy will expire in 1 hour. |
`conditions` |
`list`
A list of conditions as described in the |
`client` |
(Optional) The client to use. If not passed, falls back to the |

Returns |
|
|---|---|
Type |
Description |
`dict` |
A dictionary of (form field name, form field value) of form fields that should be added to your HTML upload form in order to attach the signature. |

### get_blob

```
get_blob(
blob_name,
client=None,
encryption_key=None,
generation=None,
if_etag_match=None,
if_etag_not_match=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
soft_deleted=None,
**kwargs
)
```


Get a blob object by name.

See a [code sample](https://cloud.google.com/storage/docs/samples/storage-get-metadata#storage_get_metadata-python)
on how to retrieve metadata of an object.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`blob_name` |
`str`
The name of the blob to retrieve. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`encryption_key` |
`bytes`
(Optional) 32 byte encryption key for customer-supplied encryption. See |
`generation` |
`long`
(Optional) If present, selects a specific revision of this object. |
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
(Optional) If True, looks for a soft-deleted object. Will only return the object metadata if the object exists and is in a soft-deleted state. Object |

Returns |
|
|---|---|
Type |
Description |
|
The blob object if it exists, otherwise None. |

### get_iam_policy

```
get_iam_policy(
client=None,
requested_policy_version=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Retrieve the IAM policy for the bucket.

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/buckets/getIamPolicy)
and a [code sample](https://cloud.google.com/storage/docs/samples/storage-view-bucket-iam-members#storage_view_bucket_iam_members-python).

If `user_project`

is set, bills the API request to that project.

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

### get_logging

`get_logging()`


Return info about access logging for this bucket.

See [https://cloud.google.com/storage/docs/access-logs#status](https://cloud.google.com/storage/docs/access-logs#status)

Returns |
|
|---|---|
Type |
Description |
`dict or None` |
a dict w/ keys, `logBucket` and `logObjectPrefix` (if logging is enabled), or None (if not). |

### get_notification

```
get_notification(
notification_id,
client=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Get Pub / Sub notification for this bucket.

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/notifications/get)
and a [code sample](https://cloud.google.com/storage/docs/samples/storage-print-pubsub-bucket-notification#storage_print_pubsub_bucket_notification-python).

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`notification_id` |
`str`
The notification id to retrieve the notification configuration. |
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
notification instance. |

### list_blobs

```
list_blobs(
max_results=None,
page_token=None,
prefix=None,
delimiter=None,
start_offset=None,
end_offset=None,
include_trailing_delimiter=None,
versions=None,
projection="noAcl",
fields=None,
client=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
match_glob=None,
include_folders_as_prefixes=None,
soft_deleted=None,
page_size=None,
)
```


Return an iterator used to find blobs in the bucket.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`max_results` |
`int`
(Optional) The maximum number of blobs to return. |
`page_token` |
`str`
(Optional) If present, return the next batch of blobs, using the value, which must correspond to the |
`prefix` |
`str`
(Optional) Prefix used to filter blobs. |
`delimiter` |
`str`
(Optional) Delimiter, used with |
`start_offset` |
`str`
(Optional) Filter results to objects whose names are lexicographically equal to or after |
`end_offset` |
`str`
(Optional) Filter results to objects whose names are lexicographically before |
`include_trailing_delimiter` |
`boolean`
(Optional) If true, objects that end in exactly one instance of |
`versions` |
`bool`
(Optional) Whether object versions should be returned as separate blobs. |
`projection` |
`str`
(Optional) If used, must be 'full' or 'noAcl'. Defaults to |
`fields` |
`str`
(Optional) Selector specifying which fields to include in a partial response. Must be a list of fields. For example to get a partial response with just the next page token and the name and language of each blob returned: |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`match_glob` |
`str`
(Optional) A glob pattern used to filter results (for example, foo*bar). The string value must be UTF-8 encoded. See: |
`soft_deleted` |
`bool`
(Optional) If true, only soft-deleted objects will be listed as distinct results in order of increasing generation number. This parameter can only be used successfully if the bucket has a soft delete policy. Note |
`page_size` |
`int`
(Optional) Maximum number of blobs to return in each page. Defaults to a value set by the API. |

Returns |
|
|---|---|
Type |
Description |
|
Iterator of all
|

### list_notifications

```
list_notifications(
client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


List Pub / Sub notifications for this bucket.

See:
[https://cloud.google.com/storage/docs/json_api/v1/notifications/list](https://cloud.google.com/storage/docs/json_api/v1/notifications/list)

If `user_project`

is set, bills the API request to that project.

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
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Returns |
|
|---|---|
Type |
Description |
`list of ` |
notification instances |

### lock_retention_policy

```
lock_retention_policy(
client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


Lock the bucket's retention policy.

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
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if the bucket has no metageneration (i.e., new or never reloaded); if the bucket has no retention policy assigned; if the bucket's retention policy is already locked. |

### make_private

```
make_private(
recursive=False,
future=False,
client=None,
timeout=60,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Update bucket's ACL, revoking read access for anonymous users.

Parameters |
|
|---|---|
Name |
Description |
`recursive` |
`bool`
If True, this will make all blobs inside the bucket private as well. |
`future` |
`bool`
If True, this will make all objects created in the future private as well. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration does not match the given value. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `recursive` is True, and the bucket contains more than 256 blobs. This is to prevent extremely long runtime of this method. For such buckets, iterate over the blobs returned by `list_blobs` and call
|

### make_public

```
make_public(
recursive=False,
future=False,
client=None,
timeout=60,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Update bucket's ACL, granting read access to anonymous users.

Parameters |
|
|---|---|
Name |
Description |
`recursive` |
`bool`
If True, this will make all blobs inside the bucket public as well. |
`future` |
`bool`
If True, this will make all objects created in the future public as well. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration does not match the given value. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `recursive` is True, and the bucket contains more than 256 blobs. This is to prevent extremely long runtime of this method. For such buckets, iterate over the blobs returned by `list_blobs` and call
|

### move_blob

```
move_blob(
blob,
new_name,
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


Move a blob to a new name atomically.

If `user_project`

is set on the bucket, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`blob` |
The blob to be renamed. |
`new_name` |
`str`
The new name for this blob. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`int`
(Optional) See :ref: |
`if_generation_not_match` |
`int`
(Optional) See :ref: |
`if_metageneration_match` |
`int`
(Optional) See :ref: |
`if_metageneration_not_match` |
`int`
(Optional) See :ref: |
`if_source_generation_match` |
`int`
(Optional) Makes the operation conditional on whether the source object's generation matches the given value. |
`if_source_generation_not_match` |
`int`
(Optional) Makes the operation conditional on whether the source object's generation does not match the given value. |
`if_source_metageneration_match` |
`int`
(Optional) Makes the operation conditional on whether the source object's current metageneration matches the given value. |
`if_source_metageneration_not_match` |
`int`
(Optional) Makes the operation conditional on whether the source object's current metageneration does not match the given value. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry`
(Optional) How to retry the RPC. See |

Returns |
|
|---|---|
Type |
Description |
|
The newly-moved blob. |

### notification

```
notification(
topic_name=None,
topic_project=None,
custom_attributes=None,
event_types=None,
blob_name_prefix=None,
payload_format="NONE",
notification_id=None,
)
```


Factory: create a notification resource for the bucket.

See: `.BucketNotification`

for parameters.

### patch

```
patch(
client=None,
timeout=60,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
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
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration does not match the given value. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

### path_helper

`path_helper(bucket_name)`


Relative URL path for a bucket.

Parameter |
|
|---|---|
Name |
Description |
`bucket_name` |
`str`
The bucket name in the path. |

Returns |
|
|---|---|
Type |
Description |
`str` |
The relative URL path for `bucket_name` . |

### reload

```
reload(
client=None,
projection="noAcl",
timeout=60,
if_etag_match=None,
if_etag_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
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
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_etag_match` |
`Union[str, Set[str]]`
(Optional) Make the operation conditional on whether the bucket's current ETag matches the given value. |
`if_etag_not_match` |
`Union[str, Set[str]])`
(Optional) Make the operation conditional on whether the bucket's current ETag does not match the given value. |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the bucket's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the bucket's current metageneration does not match the given value. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`soft_deleted` |
`bool`
(Optional) If True, looks for a soft-deleted bucket. Will only return the bucket metadata if the bucket exists and is in a soft-deleted state. The bucket |

### rename_blob

```
rename_blob(
blob,
new_name,
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


Rename the given blob using copy and delete operations.

If `user_project`

is set, bills the API request to that project.

Effectively, copies blob to the same bucket with a new name, then deletes the blob.

Parameters |
|
|---|---|
Name |
Description |
`blob` |
The blob to be renamed. |
`new_name` |
`str`
The new name for this blob. |
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
(Optional) Makes the operation conditional on whether the source object's generation matches the given value. Also used in the (implied) delete request. |
`if_source_generation_not_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's generation does not match the given value. Also used in the (implied) delete request. |
`if_source_metageneration_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's current metageneration matches the given value. Also used in the (implied) delete request. |
`if_source_metageneration_not_match` |
`long`
(Optional) Makes the operation conditional on whether the source object's current metageneration does not match the given value. Also used in the (implied) delete request. |
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
|
The newly-renamed blob. |

### restore_blob

```
restore_blob(
blob_name,
client=None,
generation=None,
copy_source_acl=None,
projection=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Restores a soft-deleted object.

If `user_project`

is set on the bucket, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`blob_name` |
`str`
The name of the blob to be restored. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`generation` |
`int`
Selects the specific revision of the object. |
`copy_source_acl` |
`bool`
(Optional) If true, copy the soft-deleted object's access controls. |
`projection` |
`str`
(Optional) Specifies the set of properties to return. If used, must be 'full' or 'noAcl'. |
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
(Optional) How to retry the RPC. The default value is |

Returns |
|
|---|---|
Type |
Description |
|
The restored Blob. |

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

See
[https://cloud.google.com/storage/docs/json_api/v1/buckets/setIamPolicy](https://cloud.google.com/storage/docs/json_api/v1/buckets/setIamPolicy)

If `user_project`

is set, bills the API request to that project.

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

See
[https://cloud.google.com/storage/docs/json_api/v1/buckets/testIamPermissions](https://cloud.google.com/storage/docs/json_api/v1/buckets/testIamPermissions)

If `user_project`

is set, bills the API request to that project.

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
timeout=60,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
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
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`if_metageneration_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration matches the given value. |
`if_metageneration_not_match` |
`long`
(Optional) Make the operation conditional on whether the blob's current metageneration does not match the given value. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |