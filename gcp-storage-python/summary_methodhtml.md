---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/summary_method.html
fetched_at: 2026-02-09T09:35:41.492354
---

# Package Methods (3.8.0)

Summary of entries of Methods for storage.

### google.cloud.storage.retry.is_etag_in_data

`is_etag_in_data(data)`


Return True if an etag is contained in the request body.

### google.cloud.storage.retry.is_etag_in_json

`is_etag_in_json(data)`


`is_etag_in_json`

is supported for backwards-compatibility reasons only;
please use `is_etag_in_data`

instead.

### google.cloud.storage.retry.is_generation_specified

`is_generation_specified(query_params)`


Return True if generation or if_generation_match is specified.

See more: [google.cloud.storage.retry.is_generation_specified](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.retry#google_cloud_storage_retry_is_generation_specified)

### google.cloud.storage.retry.is_metageneration_specified

`is_metageneration_specified(query_params)`


Return True if if_metageneration_match is specified.

See more: [google.cloud.storage.retry.is_metageneration_specified](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.retry#google_cloud_storage_retry_is_metageneration_specified)

### google.cloud.storage.transfer_manager.download_chunks_concurrently

```
download_chunks_concurrently(
blob,
filename,
chunk_size=33554432,
download_kwargs=None,
deadline=None,
worker_type="process",
max_workers=8,
*,
crc32c_checksum=True
)
```


Download a single file in chunks, concurrently.

See more: [google.cloud.storage.transfer_manager.download_chunks_concurrently](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager#google_cloud_storage_transfer_manager_download_chunks_concurrently)

### google.cloud.storage.transfer_manager.download_many

```
download_many(
blob_file_pairs,
download_kwargs=None,
threads=None,
deadline=None,
raise_exception=False,
worker_type="process",
max_workers=8,
*,
skip_if_exists=False
)
```


Download many blobs concurrently via a worker pool.

See more: [google.cloud.storage.transfer_manager.download_many](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager#google_cloud_storage_transfer_manager_download_many)

### google.cloud.storage.transfer_manager.download_many_to_path

```
download_many_to_path(
bucket,
blob_names,
destination_directory="",
blob_name_prefix="",
download_kwargs=None,
threads=None,
deadline=None,
create_directories=True,
raise_exception=False,
worker_type="process",
max_workers=8,
*,
skip_if_exists=False
)
```


Download many files concurrently by their blob names.

See more: [google.cloud.storage.transfer_manager.download_many_to_path](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager#google_cloud_storage_transfer_manager_download_many_to_path)

### google.cloud.storage.transfer_manager.upload_chunks_concurrently

```
upload_chunks_concurrently(
filename,
blob,
content_type=None,
chunk_size=33554432,
deadline=None,
worker_type="process",
max_workers=8,
*,
checksum="auto",
timeout=60,
retry=google.api_core.retry.retry_unary.Retry
)
```


Upload a single file in chunks, concurrently.

See more: [google.cloud.storage.transfer_manager.upload_chunks_concurrently](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager#google_cloud_storage_transfer_manager_upload_chunks_concurrently)

### google.cloud.storage.transfer_manager.upload_many

```
upload_many(
file_blob_pairs,
skip_if_exists=False,
upload_kwargs=None,
threads=None,
deadline=None,
raise_exception=False,
worker_type="process",
max_workers=8,
)
```


Upload many files concurrently via a worker pool.

### google.cloud.storage.transfer_manager.upload_many_from_filenames

```
upload_many_from_filenames(
bucket,
filenames,
source_directory="",
blob_name_prefix="",
skip_if_exists=False,
blob_constructor_kwargs=None,
upload_kwargs=None,
threads=None,
deadline=None,
raise_exception=False,
worker_type="process",
max_workers=8,
*,
additional_blob_attributes=None
)
```


Upload many files concurrently by their filenames.

See more: [google.cloud.storage.transfer_manager.upload_many_from_filenames](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.transfer_manager#google_cloud_storage_transfer_manager_upload_many_from_filenames)

### google.cloud.storage.acl.ACL.add_entity

`add_entity(entity)`


Add an entity to the ACL.

See more: [google.cloud.storage.acl.ACL.add_entity](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_add_entity)

### google.cloud.storage.acl.ACL.all

`all()`


Factory method for an Entity representing all users.

See more: [google.cloud.storage.acl.ACL.all](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_all)

### google.cloud.storage.acl.ACL.all_authenticated

`all_authenticated()`


Factory method for an Entity representing all authenticated users.

### google.cloud.storage.acl.ACL.clear

```
clear(
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Remove all ACL entries.

See more: [google.cloud.storage.acl.ACL.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_clear)

### google.cloud.storage.acl.ACL.domain

`domain(domain)`


Factory method for a domain Entity.

See more: [google.cloud.storage.acl.ACL.domain](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_domain)

### google.cloud.storage.acl.ACL.entity

`entity(entity_type, identifier=None)`


Factory method for creating an Entity.

See more: [google.cloud.storage.acl.ACL.entity](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_entity)

### google.cloud.storage.acl.ACL.entity_from_dict

`entity_from_dict(entity_dict)`


Build an _ACLEntity object from a dictionary of data.

### google.cloud.storage.acl.ACL.get_entities

`get_entities()`


Get a list of all Entity objects.

### google.cloud.storage.acl.ACL.get_entity

`get_entity(entity, default=None)`


Gets an entity object from the ACL.

See more: [google.cloud.storage.acl.ACL.get_entity](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_get_entity)

### google.cloud.storage.acl.ACL.group

`group(identifier)`


Factory method for a group Entity.

See more: [google.cloud.storage.acl.ACL.group](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_group)

### google.cloud.storage.acl.ACL.has_entity

`has_entity(entity)`


Returns whether or not this ACL has any entries for an entity.

See more: [google.cloud.storage.acl.ACL.has_entity](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_has_entity)

### google.cloud.storage.acl.ACL.reload

`reload(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Reload the ACL data from Cloud Storage.

See more: [google.cloud.storage.acl.ACL.reload](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_reload)

### google.cloud.storage.acl.ACL.reset

`reset()`


Remove all entities from the ACL, and clear the `loaded`

flag.

See more: [google.cloud.storage.acl.ACL.reset](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_reset)

### google.cloud.storage.acl.ACL.save

```
save(
acl=None,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Save this ACL for the current bucket.

See more: [google.cloud.storage.acl.ACL.save](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_save)

### google.cloud.storage.acl.ACL.save_predefined

```
save_predefined(
predefined,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Save this ACL for the current bucket using a predefined ACL.

### google.cloud.storage.acl.ACL.user

`user(identifier)`


Factory method for a user Entity.

See more: [google.cloud.storage.acl.ACL.user](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL#google_cloud_storage_acl_ACL_user)

### google.cloud.storage.acl.ACL.validate_predefined

`validate_predefined(predefined)`


Ensures predefined is in list of predefined json values .

### google.cloud.storage.acl.ObjectACL.clear

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

See more: [google.cloud.storage.acl.ObjectACL.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ObjectACL#google_cloud_storage_acl_ObjectACL_clear)

### google.cloud.storage.acl.ObjectACL.save

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

See more: [google.cloud.storage.acl.ObjectACL.save](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ObjectACL#google_cloud_storage_acl_ObjectACL_save)

### google.cloud.storage.acl.ObjectACL.save_predefined

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

See more: [google.cloud.storage.acl.ObjectACL.save_predefined](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ObjectACL#google_cloud_storage_acl_ObjectACL_save_predefined)

### google.cloud.storage.batch.Batch.current

`current()`


Return the topmost batch, or None.

See more: [google.cloud.storage.batch.Batch.current](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.batch.Batch#google_cloud_storage_batch_Batch_current)

### google.cloud.storage.batch.Batch.finish

`finish(raise_exception=True)`


Submit a single `multipart/mixed`

request with deferred requests.

See more: [google.cloud.storage.batch.Batch.finish](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.batch.Batch#google_cloud_storage_batch_Batch_finish)

### google.cloud.storage.batch.MIMEApplicationHTTP

`MIMEApplicationHTTP(method, uri, headers, body)`


Create an application/* type MIME document.

### google.cloud.storage.blob.Blob

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

See more: [google.cloud.storage.blob.Blob](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_Blob)

### google.cloud.storage.blob.Blob.compose

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

See more: [google.cloud.storage.blob.Blob.compose](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_compose)

### google.cloud.storage.blob.Blob.create_resumable_upload_session

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

See more: [google.cloud.storage.blob.Blob.create_resumable_upload_session](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_create_resumable_upload_session)

### google.cloud.storage.blob.Blob.delete

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

See more: [google.cloud.storage.blob.Blob.delete](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_delete)

### google.cloud.storage.blob.Blob.download_as_bytes

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

### google.cloud.storage.blob.Blob.download_as_string

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

### google.cloud.storage.blob.Blob.download_as_text

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

### google.cloud.storage.blob.Blob.download_to_file

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

### google.cloud.storage.blob.Blob.download_to_filename

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

See more: [google.cloud.storage.blob.Blob.download_to_filename](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_download_to_filename)

### google.cloud.storage.blob.Blob.exists

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

See more: [google.cloud.storage.blob.Blob.exists](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_exists)

### google.cloud.storage.blob.Blob.from_string

`from_string(uri, client=None)`


(Deprecated) Get a constructor for blob object by URI.

### google.cloud.storage.blob.Blob.from_uri

`from_uri(uri, client=None)`


Get a constructor for blob object by URI.

See more: [google.cloud.storage.blob.Blob.from_uri](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_from_uri)

### google.cloud.storage.blob.Blob.generate_signed_url

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

See more: [google.cloud.storage.blob.Blob.generate_signed_url](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_generate_signed_url)

### google.cloud.storage.blob.Blob.get_iam_policy

```
get_iam_policy(
client=None,
requested_policy_version=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Retrieve the IAM policy for the object.

### google.cloud.storage.blob.Blob.make_private

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

### google.cloud.storage.blob.Blob.make_public

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

### google.cloud.storage.blob.Blob.open

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

See more: [google.cloud.storage.blob.Blob.open](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_open)

### google.cloud.storage.blob.Blob.patch

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

See more: [google.cloud.storage.blob.Blob.patch](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_patch)

### google.cloud.storage.blob.Blob.path_helper

`path_helper(bucket_path, blob_name)`


Relative URL path for a blob.

### google.cloud.storage.blob.Blob.reload

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

See more: [google.cloud.storage.blob.Blob.reload](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_reload)

### google.cloud.storage.blob.Blob.rewrite

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

See more: [google.cloud.storage.blob.Blob.rewrite](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_rewrite)

### google.cloud.storage.blob.Blob.set_iam_policy

```
set_iam_policy(
policy,
client=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Update the IAM policy for the bucket.

### google.cloud.storage.blob.Blob.test_iam_permissions

```
test_iam_permissions(
permissions, client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


API call: test permissions.

See more: [google.cloud.storage.blob.Blob.test_iam_permissions](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_test_iam_permissions)

### google.cloud.storage.blob.Blob.update

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

See more: [google.cloud.storage.blob.Blob.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_update)

### google.cloud.storage.blob.Blob.update_storage_class

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


Update blob's storage class via a rewrite-in-place.

See more: [google.cloud.storage.blob.Blob.update_storage_class](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_update_storage_class)

### google.cloud.storage.blob.Blob.upload_from_file

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

### google.cloud.storage.blob.Blob.upload_from_filename

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

See more: [google.cloud.storage.blob.Blob.upload_from_filename](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Blob#google_cloud_storage_blob_Blob_upload_from_filename)

### google.cloud.storage.blob.Blob.upload_from_string

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

### google.cloud.storage.blob.Retention.clear

`clear()`


API documentation for `storage.blob.Retention.clear`

method.

### google.cloud.storage.blob.Retention.copy

`copy()`


API documentation for `storage.blob.Retention.copy`

method.

See more: [google.cloud.storage.blob.Retention.copy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_copy)

### google.cloud.storage.blob.Retention.from_api_repr

`from_api_repr(resource, blob)`


Factory: construct instance from resource.

### google.cloud.storage.blob.Retention.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

### google.cloud.storage.blob.Retention.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

See more: [google.cloud.storage.blob.Retention.get](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_get)

### google.cloud.storage.blob.Retention.items

`items()`


API documentation for `storage.blob.Retention.items`

method.

### google.cloud.storage.blob.Retention.keys

`keys()`


API documentation for `storage.blob.Retention.keys`

method.

See more: [google.cloud.storage.blob.Retention.keys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_keys)

### google.cloud.storage.blob.Retention.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

See more: [google.cloud.storage.blob.Retention.pop](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention#google_cloud_storage_blob_Retention_pop)

### google.cloud.storage.blob.Retention.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

### google.cloud.storage.blob.Retention.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

### google.cloud.storage.blob.Retention.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

### google.cloud.storage.blob.Retention.values

`values()`


API documentation for `storage.blob.Retention.values`

method.

### google.cloud.storage.bucket.Bucket

`Bucket(client, name=None, user_project=None, generation=None)`


property `name`

Get the bucket's name.

See more: [google.cloud.storage.bucket.Bucket](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_Bucket)

### google.cloud.storage.bucket.Bucket.add_lifecycle_abort_incomplete_multipart_upload_rule

`add_lifecycle_abort_incomplete_multipart_upload_rule(**kw)`


Add a "abort incomplete multipart upload" rule to lifecycle rules.

See more: [google.cloud.storage.bucket.Bucket.add_lifecycle_abort_incomplete_multipart_upload_rule](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_add_lifecycle_abort_incomplete_multipart_upload_rule)

### google.cloud.storage.bucket.Bucket.add_lifecycle_delete_rule

`add_lifecycle_delete_rule(**kw)`


Add a "delete" rule to lifecycle rules configured for this bucket.

See more: [google.cloud.storage.bucket.Bucket.add_lifecycle_delete_rule](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_add_lifecycle_delete_rule)

### google.cloud.storage.bucket.Bucket.add_lifecycle_set_storage_class_rule

`add_lifecycle_set_storage_class_rule(storage_class, **kw)`


Add a "set storage class" rule to lifecycle rules.

See more: [google.cloud.storage.bucket.Bucket.add_lifecycle_set_storage_class_rule](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_add_lifecycle_set_storage_class_rule)

### google.cloud.storage.bucket.Bucket.blob

```
blob(
blob_name, chunk_size=None, encryption_key=None, kms_key_name=None, generation=None
)
```


Factory constructor for blob object.

See more: [google.cloud.storage.bucket.Bucket.blob](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_blob)

### google.cloud.storage.bucket.Bucket.clear_lifecycle_rules

`clear_lifecycle_rules()`


Clear lifecycle rules configured for this bucket.

See more: [google.cloud.storage.bucket.Bucket.clear_lifecycle_rules](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_clear_lifecycle_rules)

### google.cloud.storage.bucket.Bucket.clear_lifecyle_rules

`clear_lifecyle_rules()`


Deprecated alias for clear_lifecycle_rules.

See more: [google.cloud.storage.bucket.Bucket.clear_lifecyle_rules](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_clear_lifecyle_rules)

### google.cloud.storage.bucket.Bucket.configure_website

`configure_website(main_page_suffix=None, not_found_page=None)`


Configure website-related properties.

See more: [google.cloud.storage.bucket.Bucket.configure_website](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_configure_website)

### google.cloud.storage.bucket.Bucket.copy_blob

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

### google.cloud.storage.bucket.Bucket.create

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

### google.cloud.storage.bucket.Bucket.delete

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

### google.cloud.storage.bucket.Bucket.delete_blob

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

### google.cloud.storage.bucket.Bucket.delete_blobs

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

### google.cloud.storage.bucket.Bucket.disable_logging

`disable_logging()`


Disable access logging for this bucket.

See more: [google.cloud.storage.bucket.Bucket.disable_logging](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_disable_logging)

### google.cloud.storage.bucket.Bucket.disable_website

`disable_website()`


Disable the website configuration for this bucket.

See more: [google.cloud.storage.bucket.Bucket.disable_website](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_disable_website)

### google.cloud.storage.bucket.Bucket.enable_logging

`enable_logging(bucket_name, object_prefix="")`


Enable access logging for this bucket.

### google.cloud.storage.bucket.Bucket.exists

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

### google.cloud.storage.bucket.Bucket.from_string

`from_string(uri, client=None)`


Get a constructor for bucket object by URI.

### google.cloud.storage.bucket.Bucket.from_uri

`from_uri(uri, client=None)`


Get a constructor for bucket object by URI.

### google.cloud.storage.bucket.Bucket.generate_signed_url

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

See more: [google.cloud.storage.bucket.Bucket.generate_signed_url](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_generate_signed_url)

### google.cloud.storage.bucket.Bucket.generate_upload_policy

`generate_upload_policy(conditions, expiration=None, client=None)`


Create a signed upload policy for uploading objects.

See more: [google.cloud.storage.bucket.Bucket.generate_upload_policy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_generate_upload_policy)

### google.cloud.storage.bucket.Bucket.get_blob

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

### google.cloud.storage.bucket.Bucket.get_iam_policy

```
get_iam_policy(
client=None,
requested_policy_version=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Retrieve the IAM policy for the bucket.

### google.cloud.storage.bucket.Bucket.get_logging

`get_logging()`


Return info about access logging for this bucket.

### google.cloud.storage.bucket.Bucket.get_notification

```
get_notification(
notification_id,
client=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Get Pub / Sub notification for this bucket.

See more: [google.cloud.storage.bucket.Bucket.get_notification](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_get_notification)

### google.cloud.storage.bucket.Bucket.list_blobs

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

### google.cloud.storage.bucket.Bucket.list_notifications

```
list_notifications(
client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


List Pub / Sub notifications for this bucket.

See more: [google.cloud.storage.bucket.Bucket.list_notifications](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_list_notifications)

### google.cloud.storage.bucket.Bucket.lock_retention_policy

```
lock_retention_policy(
client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


Lock the bucket's retention policy.

See more: [google.cloud.storage.bucket.Bucket.lock_retention_policy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_lock_retention_policy)

### google.cloud.storage.bucket.Bucket.make_private

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

### google.cloud.storage.bucket.Bucket.make_public

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

### google.cloud.storage.bucket.Bucket.move_blob

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

### google.cloud.storage.bucket.Bucket.notification

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

### google.cloud.storage.bucket.Bucket.patch

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

See more: [google.cloud.storage.bucket.Bucket.patch](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_patch)

### google.cloud.storage.bucket.Bucket.path_helper

`path_helper(bucket_name)`


Relative URL path for a bucket.

### google.cloud.storage.bucket.Bucket.reload

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

### google.cloud.storage.bucket.Bucket.rename_blob

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

### google.cloud.storage.bucket.Bucket.restore_blob

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

### google.cloud.storage.bucket.Bucket.set_iam_policy

```
set_iam_policy(
policy,
client=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Update the IAM policy for the bucket.

### google.cloud.storage.bucket.Bucket.test_iam_permissions

```
test_iam_permissions(
permissions, client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


API call: test permissions.

See more: [google.cloud.storage.bucket.Bucket.test_iam_permissions](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.Bucket#google_cloud_storage_bucket_Bucket_test_iam_permissions)

### google.cloud.storage.bucket.Bucket.update

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

### google.cloud.storage.bucket.IAMConfiguration.clear

`clear()`


API documentation for `storage.bucket.IAMConfiguration.clear`

method.

See more: [google.cloud.storage.bucket.IAMConfiguration.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_clear)

### google.cloud.storage.bucket.IAMConfiguration.copy

`copy()`


API documentation for `storage.bucket.IAMConfiguration.copy`

method.

### google.cloud.storage.bucket.IAMConfiguration.from_api_repr

`from_api_repr(resource, bucket)`


Factory: construct instance from resource.

See more: [google.cloud.storage.bucket.IAMConfiguration.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_from_api_repr)

### google.cloud.storage.bucket.IAMConfiguration.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

See more: [google.cloud.storage.bucket.IAMConfiguration.fromkeys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_fromkeys)

### google.cloud.storage.bucket.IAMConfiguration.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

### google.cloud.storage.bucket.IAMConfiguration.items

`items()`


API documentation for `storage.bucket.IAMConfiguration.items`

method.

See more: [google.cloud.storage.bucket.IAMConfiguration.items](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_items)

### google.cloud.storage.bucket.IAMConfiguration.keys

`keys()`


API documentation for `storage.bucket.IAMConfiguration.keys`

method.

### google.cloud.storage.bucket.IAMConfiguration.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

### google.cloud.storage.bucket.IAMConfiguration.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

See more: [google.cloud.storage.bucket.IAMConfiguration.popitem](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_popitem)

### google.cloud.storage.bucket.IAMConfiguration.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

See more: [google.cloud.storage.bucket.IAMConfiguration.setdefault](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_setdefault)

### google.cloud.storage.bucket.IAMConfiguration.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

See more: [google.cloud.storage.bucket.IAMConfiguration.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_update)

### google.cloud.storage.bucket.IAMConfiguration.values

`values()`


API documentation for `storage.bucket.IAMConfiguration.values`

method.

See more: [google.cloud.storage.bucket.IAMConfiguration.values](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration#google_cloud_storage_bucket_IAMConfiguration_values)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.clear

`clear()`


API documentation for `storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.clear`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_clear)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.copy

`copy()`


API documentation for `storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.copy`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.copy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_copy)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.from_api_repr

`from_api_repr(resource)`


Factory: construct instance from resource.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_from_api_repr)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.fromkeys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_fromkeys)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.get](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_get)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.items

`items()`


API documentation for `storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.items`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.items](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_items)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.keys

`keys()`


API documentation for `storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.keys`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.keys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_keys)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.pop](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_pop)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.popitem](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_popitem)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.setdefault](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_setdefault)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_update)

### google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.values

`values()`


API documentation for `storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.values`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload.values](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleAbortIncompleteMultipartUpload#google_cloud_storage_bucket_LifecycleRuleAbortIncompleteMultipartUpload_values)

### google.cloud.storage.bucket.LifecycleRuleConditions.clear

`clear()`


API documentation for `storage.bucket.LifecycleRuleConditions.clear`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_clear)

### google.cloud.storage.bucket.LifecycleRuleConditions.copy

`copy()`


API documentation for `storage.bucket.LifecycleRuleConditions.copy`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.copy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_copy)

### google.cloud.storage.bucket.LifecycleRuleConditions.from_api_repr

`from_api_repr(resource)`


Factory: construct instance from resource.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_from_api_repr)

### google.cloud.storage.bucket.LifecycleRuleConditions.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.fromkeys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_fromkeys)

### google.cloud.storage.bucket.LifecycleRuleConditions.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.get](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_get)

### google.cloud.storage.bucket.LifecycleRuleConditions.items

`items()`


API documentation for `storage.bucket.LifecycleRuleConditions.items`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.items](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_items)

### google.cloud.storage.bucket.LifecycleRuleConditions.keys

`keys()`


API documentation for `storage.bucket.LifecycleRuleConditions.keys`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.keys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_keys)

### google.cloud.storage.bucket.LifecycleRuleConditions.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.pop](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_pop)

### google.cloud.storage.bucket.LifecycleRuleConditions.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.popitem](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_popitem)

### google.cloud.storage.bucket.LifecycleRuleConditions.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.setdefault](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_setdefault)

### google.cloud.storage.bucket.LifecycleRuleConditions.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_update)

### google.cloud.storage.bucket.LifecycleRuleConditions.values

`values()`


API documentation for `storage.bucket.LifecycleRuleConditions.values`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleConditions.values](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions#google_cloud_storage_bucket_LifecycleRuleConditions_values)

### google.cloud.storage.bucket.LifecycleRuleDelete.clear

`clear()`


API documentation for `storage.bucket.LifecycleRuleDelete.clear`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_clear)

### google.cloud.storage.bucket.LifecycleRuleDelete.copy

`copy()`


API documentation for `storage.bucket.LifecycleRuleDelete.copy`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.copy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_copy)

### google.cloud.storage.bucket.LifecycleRuleDelete.from_api_repr

`from_api_repr(resource)`


Factory: construct instance from resource.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_from_api_repr)

### google.cloud.storage.bucket.LifecycleRuleDelete.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.fromkeys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_fromkeys)

### google.cloud.storage.bucket.LifecycleRuleDelete.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.get](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_get)

### google.cloud.storage.bucket.LifecycleRuleDelete.items

`items()`


API documentation for `storage.bucket.LifecycleRuleDelete.items`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.items](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_items)

### google.cloud.storage.bucket.LifecycleRuleDelete.keys

`keys()`


API documentation for `storage.bucket.LifecycleRuleDelete.keys`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.keys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_keys)

### google.cloud.storage.bucket.LifecycleRuleDelete.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.pop](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_pop)

### google.cloud.storage.bucket.LifecycleRuleDelete.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.popitem](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_popitem)

### google.cloud.storage.bucket.LifecycleRuleDelete.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.setdefault](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_setdefault)

### google.cloud.storage.bucket.LifecycleRuleDelete.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_update)

### google.cloud.storage.bucket.LifecycleRuleDelete.values

`values()`


API documentation for `storage.bucket.LifecycleRuleDelete.values`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleDelete.values](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleDelete#google_cloud_storage_bucket_LifecycleRuleDelete_values)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.clear

`clear()`


API documentation for `storage.bucket.LifecycleRuleSetStorageClass.clear`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_clear)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.copy

`copy()`


API documentation for `storage.bucket.LifecycleRuleSetStorageClass.copy`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.copy](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_copy)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.from_api_repr

`from_api_repr(resource)`


Factory: construct instance from resource.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_from_api_repr)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.fromkeys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_fromkeys)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.get](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_get)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.items

`items()`


API documentation for `storage.bucket.LifecycleRuleSetStorageClass.items`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.items](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_items)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.keys

`keys()`


API documentation for `storage.bucket.LifecycleRuleSetStorageClass.keys`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.keys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_keys)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.pop](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_pop)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.popitem](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_popitem)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.setdefault](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_setdefault)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_update)

### google.cloud.storage.bucket.LifecycleRuleSetStorageClass.values

`values()`


API documentation for `storage.bucket.LifecycleRuleSetStorageClass.values`

method.

See more: [google.cloud.storage.bucket.LifecycleRuleSetStorageClass.values](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleSetStorageClass#google_cloud_storage_bucket_LifecycleRuleSetStorageClass_values)

### google.cloud.storage.bucket.SoftDeletePolicy.clear

`clear()`


API documentation for `storage.bucket.SoftDeletePolicy.clear`

method.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.clear](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_clear)

### google.cloud.storage.bucket.SoftDeletePolicy.copy

`copy()`


API documentation for `storage.bucket.SoftDeletePolicy.copy`

method.

### google.cloud.storage.bucket.SoftDeletePolicy.from_api_repr

`from_api_repr(resource, bucket)`


Factory: construct instance from resource.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_from_api_repr)

### google.cloud.storage.bucket.SoftDeletePolicy.fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.fromkeys](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_fromkeys)

### google.cloud.storage.bucket.SoftDeletePolicy.get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

### google.cloud.storage.bucket.SoftDeletePolicy.items

`items()`


API documentation for `storage.bucket.SoftDeletePolicy.items`

method.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.items](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_items)

### google.cloud.storage.bucket.SoftDeletePolicy.keys

`keys()`


API documentation for `storage.bucket.SoftDeletePolicy.keys`

method.

### google.cloud.storage.bucket.SoftDeletePolicy.pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

### google.cloud.storage.bucket.SoftDeletePolicy.popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.popitem](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_popitem)

### google.cloud.storage.bucket.SoftDeletePolicy.setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.setdefault](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_setdefault)

### google.cloud.storage.bucket.SoftDeletePolicy.update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k].

See more: [google.cloud.storage.bucket.SoftDeletePolicy.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_update)

### google.cloud.storage.bucket.SoftDeletePolicy.values

`values()`


API documentation for `storage.bucket.SoftDeletePolicy.values`

method.

See more: [google.cloud.storage.bucket.SoftDeletePolicy.values](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy#google_cloud_storage_bucket_SoftDeletePolicy_values)

### google.cloud.storage.client.Client.batch

`batch(raise_exception=True)`


Factory constructor for batch object.

See more: [google.cloud.storage.client.Client.batch](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_batch)

### google.cloud.storage.client.Client.bucket

`bucket(bucket_name, user_project=None, generation=None)`


Factory constructor for bucket object.

### google.cloud.storage.client.Client.create_anonymous_client

`create_anonymous_client()`


Factory: return client with anonymous credentials.

See more: [google.cloud.storage.client.Client.create_anonymous_client](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_create_anonymous_client)

### google.cloud.storage.client.Client.create_bucket

```
create_bucket(
bucket_or_name,
requester_pays=None,
project=None,
user_project=None,
location=None,
data_locations=None,
predefined_acl=None,
predefined_default_object_acl=None,
enable_object_retention=False,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Create a new bucket via a POST request.

### google.cloud.storage.client.Client.create_hmac_key

```
create_hmac_key(
service_account_email, project_id=None, user_project=None, timeout=60, retry=None
)
```


Create an HMAC key for a service account.

See more: [google.cloud.storage.client.Client.create_hmac_key](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_create_hmac_key)

### google.cloud.storage.client.Client.download_blob_to_file

```
download_blob_to_file(
blob_or_uri,
file_obj,
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


Download the contents of a blob object or blob URI into a file-like object.

See more: [google.cloud.storage.client.Client.download_blob_to_file](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_download_blob_to_file)

### google.cloud.storage.client.Client.generate_signed_post_policy_v4

```
generate_signed_post_policy_v4(
bucket_name,
blob_name,
expiration,
conditions=None,
fields=None,
credentials=None,
virtual_hosted_style=False,
bucket_bound_hostname=None,
scheme="http",
service_account_email=None,
access_token=None,
)
```


Generate a V4 signed policy object.

See more: [google.cloud.storage.client.Client.generate_signed_post_policy_v4](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_generate_signed_post_policy_v4)

### google.cloud.storage.client.Client.get_bucket

```
get_bucket(
bucket_or_name,
timeout=60,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
*,
generation=None,
soft_deleted=None
)
```


Retrieve a bucket via a GET request.

### google.cloud.storage.client.Client.get_hmac_key_metadata

`get_hmac_key_metadata(access_id, project_id=None, user_project=None, timeout=60)`


Return a metadata instance for the given HMAC key.

See more: [google.cloud.storage.client.Client.get_hmac_key_metadata](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_get_hmac_key_metadata)

### google.cloud.storage.client.Client.get_service_account_email

```
get_service_account_email(
project=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


Get the email address of the project's GCS service account .

See more: [google.cloud.storage.client.Client.get_service_account_email](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_get_service_account_email)

### google.cloud.storage.client.Client.list_blobs

```
list_blobs(
bucket_or_name,
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
page_size=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
match_glob=None,
include_folders_as_prefixes=None,
soft_deleted=None,
)
```


Return an iterator used to find blobs in the bucket.

### google.cloud.storage.client.Client.list_buckets

```
list_buckets(
max_results=None,
page_token=None,
prefix=None,
projection="noAcl",
fields=None,
project=None,
page_size=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
*,
soft_deleted=None,
return_partial_success=None
)
```


Get all buckets in the project associated to the client.

### google.cloud.storage.client.Client.list_hmac_keys

```
list_hmac_keys(
max_results=None,
service_account_email=None,
show_deleted_keys=None,
project_id=None,
user_project=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


List HMAC keys for a project.

### google.cloud.storage.client.Client.lookup_bucket

```
lookup_bucket(
bucket_name,
timeout=60,
if_metageneration_match=None,
if_metageneration_not_match=None,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Get a bucket by name, returning None if not found.

### google.cloud.storage.client.Client.restore_bucket

```
restore_bucket(
bucket_name,
generation,
projection="noAcl",
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.api_core.retry.retry_unary.Retry,
)
```


Restores a soft-deleted bucket.

### google.cloud.storage.client.Client.update_user_agent

`update_user_agent(user_agent)`


Update the user-agent string for this client.

See more: [google.cloud.storage.client.Client.update_user_agent](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client#google_cloud_storage_client_Client_update_user_agent)

### google.cloud.storage.fileio.BlobReader.close

`close()`


Flush and close the IO object.

### google.cloud.storage.fileio.BlobReader.read

`read(size=-1)`


Read and return up to n bytes.

### google.cloud.storage.fileio.BlobReader.read1

`read1(size=-1)`


Read and return up to n bytes, with at most one read() call to the underlying raw stream.

### google.cloud.storage.fileio.BlobReader.readable

`readable()`


Return whether object was opened for reading.

### google.cloud.storage.fileio.BlobReader.seek

`seek(pos, whence=0)`


Seek within the blob.

### google.cloud.storage.fileio.BlobReader.seekable

`seekable()`


Return whether object supports random access.

### google.cloud.storage.fileio.BlobReader.writable

`writable()`


Return whether object was opened for writing.

### google.cloud.storage.fileio.BlobWriter.close

`close()`


Flush and close the IO object.

### google.cloud.storage.fileio.BlobWriter.flush

`flush()`


Flush write buffers, if applicable.

### google.cloud.storage.fileio.BlobWriter.readable

`readable()`


Return whether object was opened for reading.

### google.cloud.storage.fileio.BlobWriter.seekable

`seekable()`


Return whether object supports random access.

### google.cloud.storage.fileio.BlobWriter.tell

`tell()`


Return current stream position.

### google.cloud.storage.fileio.BlobWriter.terminate

`terminate()`


Cancel the ResumableUpload.

### google.cloud.storage.fileio.BlobWriter.writable

`writable()`


Return whether object was opened for writing.

### google.cloud.storage.fileio.BlobWriter.write

`write(b)`


Write the given buffer to the IO stream.

### google.cloud.storage.fileio.SlidingBuffer.__len__

`__len__()`


Determine the size of the buffer by seeking to the end.

### google.cloud.storage.fileio.SlidingBuffer.flush

`flush()`


Delete already-read data (all data to the left of the position).

### google.cloud.storage.fileio.SlidingBuffer.read

`read(size=-1)`


Read and move the cursor.

### google.cloud.storage.fileio.SlidingBuffer.seek

`seek(pos)`


Seek to a position (backwards only) within the internal buffer.

### google.cloud.storage.fileio.SlidingBuffer.tell

`tell()`


Report how many bytes have been read from the buffer in total.

### google.cloud.storage.fileio.SlidingBuffer.write

`write(b)`


Append to the end of the buffer without changing the position.

### google.cloud.storage.hmac_key.HMACKeyMetadata.delete

`delete(timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Delete the key from Cloud Storage.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.delete](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_delete)

### google.cloud.storage.hmac_key.HMACKeyMetadata.exists

`exists(timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Determine whether or not the key for this metadata exists.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.exists](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_exists)

### google.cloud.storage.hmac_key.HMACKeyMetadata.reload

`reload(timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Reload properties from Cloud Storage.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.reload](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_reload)

### google.cloud.storage.hmac_key.HMACKeyMetadata.update

`update(timeout=60, retry=google.cloud.storage.retry.ConditionalRetryPolicy)`


Save writable properties to Cloud Storage.

See more: [google.cloud.storage.hmac_key.HMACKeyMetadata.update](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata#google_cloud_storage_hmac_key_HMACKeyMetadata_update)

### google.cloud.storage.notification.BucketNotification.create

`create(client=None, timeout=60, retry=None)`


API wrapper: create the notification.

See more: [google.cloud.storage.notification.BucketNotification.create](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_create)

### google.cloud.storage.notification.BucketNotification.delete

`delete(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Delete this notification.

See more: [google.cloud.storage.notification.BucketNotification.delete](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_delete)

### google.cloud.storage.notification.BucketNotification.exists

`exists(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Test whether this notification exists.

See more: [google.cloud.storage.notification.BucketNotification.exists](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_exists)

### google.cloud.storage.notification.BucketNotification.from_api_repr

`from_api_repr(resource, bucket)`


Construct an instance from the JSON repr returned by the server.

See more: [google.cloud.storage.notification.BucketNotification.from_api_repr](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_from_api_repr)

### google.cloud.storage.notification.BucketNotification.reload

`reload(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Update this notification from the server configuration.

See more: [google.cloud.storage.notification.BucketNotification.reload](https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification#google_cloud_storage_notification_BucketNotification_reload)