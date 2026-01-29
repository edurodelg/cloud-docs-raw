---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/summary_class
fetched_at: 2026-01-29T15:33:56.629400
---

# Package Classes (3.7.0)

Summary of entries of Classes for storage.

## Classes

[ACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL)

Container class representing a list of access controls.

[BucketACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.BucketACL)

An ACL specifically for a bucket.

[DefaultObjectACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.DefaultObjectACL)

A class representing the default object ACL for a bucket.

[ObjectACL](/python/docs/reference/storage/latest/google.cloud.storage.acl.ObjectACL)

An ACL specifically for a Cloud Storage object / blob.

[Batch](/python/docs/reference/storage/latest/google.cloud.storage.batch.Batch)

Proxy an underlying connection, batching up change operations.

[MIMEApplicationHTTP](/python/docs/reference/storage/latest/google.cloud.storage.batch.MIMEApplicationHTTP)

MIME type for `application/http`

.

Constructs payload from headers and body

[Blob](/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob)

A wrapper around Cloud Storage's concept of an `Object`

.

[Retention](/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention)

Map an object's retention configuration.

[Bucket](/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket)

A class representing a Bucket on Cloud Storage.

[IAMConfiguration](/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration)

Map a bucket's IAM configuration.

[LifecycleRuleAbortIncompleteMultipartUpload](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload)

Map a rule aborting incomplete multipart uploads of matching items.

The "age" lifecycle condition is the only supported condition for this rule.

[LifecycleRuleConditions](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions)

Map a single lifecycle rule for a bucket.

[LifecycleRuleDelete](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete)

Map a lifecycle rule deleting matching items.

[LifecycleRuleSetStorageClass](/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass)

Map a lifecycle rule updating storage class of matching items.

[SoftDeletePolicy](/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy)

Map a bucket's soft delete policy.

[Client](/python/docs/reference/storage/latest/google.cloud.storage.client.Client)

Client to bundle configuration needed for API requests.

[DataCorruption](/python/docs/reference/storage/latest/google.cloud.storage.exceptions.DataCorruption)

Error class for corrupt media transfers.

[InvalidResponse](/python/docs/reference/storage/latest/google.cloud.storage.exceptions.InvalidResponse)

Error class for responses which are not in the correct state.

[BlobReader](/python/docs/reference/storage/latest/google.cloud.storage.fileio.BlobReader)

A file-like object that reads from a blob.

[BlobWriter](/python/docs/reference/storage/latest/google.cloud.storage.fileio.BlobWriter)

A file-like object that writes to a blob.

[SlidingBuffer](/python/docs/reference/storage/latest/google.cloud.storage.fileio.SlidingBuffer)

A non-rewindable buffer that frees memory of chunks already consumed.

This class is necessary because `google-resumable-media-python`

expects
`tell()`

to work relative to the start of the file, not relative to a place
in an intermediate buffer. Using this class, we present an external
interface with consistent seek and tell behavior without having to actually
store bytes already sent.

Behavior of this class differs from an ordinary BytesIO buffer. `write()`

will always append to the end of the file only and not change the seek
position otherwise. `flush()`

will delete all data already read (data to the
left of the seek position). `tell()`

will report the seek position of the
buffer including all deleted data. Additionally the class implements
**len**() which will report the size of the actual underlying buffer.

This class does not attempt to implement the entire Python I/O interface.

[HMACKeyMetadata](/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata)

Metadata about an HMAC service account key withn Cloud Storage.

[BucketNotification](/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification)

Represent a single notification resource for a bucket.

See: [https://cloud.google.com/storage/docs/json_api/v1/notifications](https://cloud.google.com/storage/docs/json_api/v1/notifications)

[ConditionalRetryPolicy](/python/docs/reference/storage/latest/google.cloud.storage.retry.ConditionalRetryPolicy)

A class for use when an API call is only conditionally safe to retry.

This class is intended for use in inspecting the API call parameters of an
API call to verify that any flags necessary to make the API call idempotent
(such as specifying an `if_generation_match`

or related flag) are present.

It can be used in place of a `retry.Retry`

object, in which case
`_http.Connection.api_request`

will pass the requested api call keyword
arguments into the `conditional_predicate`

and return the `retry_policy`

if the conditions are met.

## Modules

[acl](/python/docs/reference/storage/latest/google.cloud.storage.acl)

Manage access to objects and buckets.

[batch](/python/docs/reference/storage/latest/google.cloud.storage.batch)

Batch updates / deletes of storage buckets / blobs.

A batch request is a single standard HTTP request containing multiple Cloud Storage JSON API calls. Within this main HTTP request, there are multiple parts which each contain a nested HTTP request. The body of each part is itself a complete HTTP request, with its own verb, URL, headers, and body.

Note that Cloud Storage does not support batch operations for uploading or downloading.
Additionally, the current batch design does not support library methods whose return values
depend on the response payload. See more details in the [Sending Batch Requests official guide](https://cloud.google.com/storage/docs/batch).

Examples of situations when you might want to use the Batch module:
`blob.patch()`

`blob.update()`

`blob.delete()`

`bucket.delete_blob()`

`bucket.patch()`

`bucket.update()`


[blob](/python/docs/reference/storage/latest/google.cloud.storage.blob)

Create / interact with Google Cloud Storage blobs.

[bucket](/python/docs/reference/storage/latest/google.cloud.storage.bucket)

Create / interact with Google Cloud Storage buckets.

[client](/python/docs/reference/storage/latest/google.cloud.storage.client)

Client for interacting with the Google Cloud Storage API.

[constants](/python/docs/reference/storage/latest/google.cloud.storage.constants)

Constants used across google.cloud.storage modules.

See [Python Storage Client Constants Page](https://github.com/googleapis/python-storage/blob/main/google/cloud/storage/constants.py)
for constants used across storage classes, location types, public access prevention, etc.

[exceptions](/python/docs/reference/storage/latest/google.cloud.storage.exceptions)

Exceptions raised by the library.

[fileio](/python/docs/reference/storage/latest/google.cloud.storage.fileio)

Module for file-like access of blobs, usually invoked via Blob.open().

[hmac_key](/python/docs/reference/storage/latest/google.cloud.storage.hmac_key)

Configure HMAC keys that can be used to authenticate requests to Google Cloud Storage.

[notification](/python/docs/reference/storage/latest/google.cloud.storage.notification)

Configure bucket notification resources to interact with Google Cloud Pub/Sub.

[retry](/python/docs/reference/storage/latest/google.cloud.storage.retry)

Helpers for configuring retries with exponential back-off.

[transfer_manager](/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager)

Concurrent media operations.