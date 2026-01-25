---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client.Client
fetched_at: 2026-01-25T12:21:47.872003
---

# Class Client (3.7.0)

```
Client(
project=object,
credentials=None,
_http=None,
client_info=None,
client_options=None,
use_auth_w_custom_endpoint=True,
extra_headers={},
*,
api_key=None
)
```


Client to bundle configuration needed for API requests.

## Parameters |
|
|---|---|
Name |
Description |
`project` |
`str or None`
the project which the client acts on behalf of. Will be passed when creating a topic. If not passed, falls back to the default inferred from the environment. |
`credentials` |
(Optional) The OAuth2 Credentials to use for this client. If not passed (and if no |
`_http` |
(Optional) HTTP object to make requests. Can be any object that defines |
`client_info` |
The client info used to send a user-agent string along with API requests. If |
`client_options` |
(Optional) Client options used to set user options on the client. A non-default universe domain or api endpoint should be set through client_options. |
`use_auth_w_custom_endpoint` |
`bool`
(Optional) Whether authentication is required under custom endpoints. If false, uses AnonymousCredentials and bypasses authentication. Defaults to True. Note this is only used when a custom endpoint is set in conjunction. |
`extra_headers` |
`dict`
(Optional) Custom headers to be sent with the requests attached to the client. For example, you can add custom audit logging headers. |
`api_key` |
`string`
(Optional) An API key. Mutually exclusive with any other credentials. This parameter is an alias for setting |

## Properties

### current_batch

Currently-active batch.

Returns |
|
|---|---|
Type |
Description |
|
The batch at the top of the batch stack. |

## Methods

### batch

`batch(raise_exception=True)`


Factory constructor for batch object.

Parameter |
|
|---|---|
Name |
Description |
`raise_exception` |
`bool`
(Optional) Defaults to True. If True, instead of adding exceptions to the list of return responses, the final exception will be raised. Note that exceptions are unwrapped after all operations are complete in success or failure, and only the last exception is raised. |

Returns |
|
|---|---|
Type |
Description |
|
The batch object created. |

### bucket

`bucket(bucket_name, user_project=None, generation=None)`


Factory constructor for bucket object.

Parameters |
|
|---|---|
Name |
Description |
`bucket_name` |
`str`
The name of the bucket to be instantiated. |
`user_project` |
`str`
(Optional) The project ID to be billed for API requests made via the bucket. |
`generation` |
`int`
(Optional) If present, selects a specific revision of this bucket. |

Returns |
|
|---|---|
Type |
Description |
|
The bucket object created. |

### create_anonymous_client

`create_anonymous_client()`


Factory: return client with anonymous credentials.

Returns |
|
|---|---|
Type |
Description |
|
Instance w/ anonymous credentials and no project. |

### create_bucket

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

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/buckets/insert) and a [code sample](https://cloud.google.com/storage/docs/samples/storage-create-bucket#storage_create_bucket-python).

Parameters |
|
|---|---|
Name |
Description |
`bucket_or_name` |
`Union[ `
The bucket resource to pass or name to create. |
`requester_pays` |
`bool`
DEPRECATED. Use Bucket().requester_pays instead. (Optional) Whether requester pays for API requests for this bucket and its blobs. |
`project` |
`str`
(Optional) The project under which the bucket is to be created. If not passed, uses the project set on the client. |
`user_project` |
`str`
(Optional) The project ID to be billed for API requests made via created bucket. |
`location` |
`str`
(Optional) The location of the bucket. If not passed, the default location, US, will be used. If specifying a dual-region, |
`data_locations` |
`list of str`
(Optional) The list of regional locations of a custom dual-region bucket. Dual-regions require exactly 2 regional locations. See: |
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
`Optional[Union[float, Tuple[float, float]]]`
The amount of time, in seconds, to wait for the server response. Can also be passed as a tuple (connect_timeout, read_timeout). See |
`retry` |
`Optional[Union[google.api_core.retry.Retry, `
How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.Conflict` |
If the bucket already exists. |

### create_hmac_key

```
create_hmac_key(
service_account_email, project_id=None, user_project=None, timeout=60, retry=None
)
```


Create an HMAC key for a service account.

Parameters |
|
|---|---|
Name |
Description |
`service_account_email` |
`str`
e-mail address of the service account |
`project_id` |
`str`
(Optional) Explicit project ID for the key. Defaults to the client's project. |
`user_project` |
`str`
(Optional) This parameter is currently ignored. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |

Returns |
|
|---|---|
Type |
Description |
`Tuple[` |
metadata for the created key, plus the bytes of the key's secret, which is an 40-character base64-encoded string. |

### download_blob_to_file

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

See [https://cloud.google.com/storage/docs/downloading-objects](https://cloud.google.com/storage/docs/downloading-objects)

Parameters |
|
|---|---|
Name |
Description |
`blob_or_uri` |
`Union[ `
The blob resource to pass or URI to download. |
`file_obj` |
`file`
A file handle to which to write the blob's data. |
`start` |
`int`
(Optional) The first byte in a range to be downloaded. |
`end` |
`int`
(Optional) The last byte in a range to be downloaded. |
`raw_download` |
`bool`
(Optional) If true, download the object without any expansion. |
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
`[Union[float, Tuple[float, float]]]`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`checksum` |
`str`
(Optional) The type of checksum to compute to verify the integrity of the object. The response headers must contain a checksum of the requested type. If the headers lack an appropriate checksum (for instance in the case of transcoded or ranged downloads where the remote service does not know the correct checksum, including downloads where chunk_size is set) an INFO-level log will be emitted. Supported values are "md5", "crc32c", "auto" and None. The default is "auto", which will try to detect if the C extension for crc32c is installed and fall back to md5 otherwise. |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`single_shot_download` |
`bool`
(Optional) If true, download the object in a single request. |

### generate_signed_post_policy_v4

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


Generate a V4 signed policy object. Generated policy object allows user to upload objects with a POST request.

Parameters |
|
|---|---|
Name |
Description |
`bucket_name` |
`str`
Bucket name. |
`blob_name` |
`str`
Object name. |
`expiration` |
`Union[Integer, datetime.datetime, datetime.timedelta]`
Policy expiration time. If a |
`conditions` |
`list`
(Optional) List of POST policy conditions, which are used to restrict what is allowed in the request. |
`fields` |
`dict`
(Optional) Additional elements to include into request. |
`credentials` |
(Optional) Credentials object with an associated private key to sign text. |
`virtual_hosted_style` |
`bool`
(Optional) If True, construct the URL relative to the bucket virtual hostname, e.g., '
|
`bucket_bound_hostname` |
`str`
(Optional) If passed, construct the URL relative to the bucket-bound hostname. Value can be bare or with a scheme, e.g., 'example.com' or ' |
`scheme` |
`str`
(Optional) If |
`service_account_email` |
`str`
(Optional) E-mail address of the service account. |
`access_token` |
`str`
(Optional) Access token for a service account. |

Exceptions |
|
|---|---|
Type |
Description |
``ValueError` |
when mutually exclusive arguments are used. |

Returns |
|
|---|---|
Type |
Description |
`dict` |
Signed POST policy. |

### get_bucket

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

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/buckets/get) and a [code sample](https://cloud.google.com/storage/docs/samples/storage-get-bucket-metadata#storage_get_bucket_metadata-python).

Parameters |
|
|---|---|
Name |
Description |
`bucket_or_name` |
`Union[ `
The bucket resource to pass or name to create. |
`timeout` |
`Optional[Union[float, Tuple[float, float]]]`
The amount of time, in seconds, to wait for the server response. Can also be passed as a tuple (connect_timeout, read_timeout). See |
`if_metageneration_match` |
`Optional[int]`
Make the operation conditional on whether the bucket's current metageneration matches the given value. |
`if_metageneration_not_match` |
`Optional[int]`
Make the operation conditional on whether the bucket's current metageneration does not match the given value. |
`retry` |
`Optional[Union[google.api_core.retry.Retry, `
How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`generation` |
`Optional[int]`
The generation of the bucket. The generation can be used to specify a specific soft-deleted version of the bucket, in conjunction with the |
`soft_deleted` |
`Optional[bool]`
If True, looks for a soft-deleted bucket. Will only return the bucket metadata if the bucket exists and is in a soft-deleted state. The bucket |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.NotFound` |
If the bucket is not found. |

### get_hmac_key_metadata

`get_hmac_key_metadata(access_id, project_id=None, user_project=None, timeout=60)`


Return a metadata instance for the given HMAC key.

Parameters |
|
|---|---|
Name |
Description |
`access_id` |
`str`
Unique ID of an existing key. |
`project_id` |
`str`
(Optional) Project ID of an existing key. Defaults to client's project. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`user_project` |
`str`
(Optional) This parameter is currently ignored. |

### get_service_account_email

```
get_service_account_email(
project=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry
)
```


Get the email address of the project's GCS service account

Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
(Optional) Project ID to use for retreiving GCS service account email address. Defaults to the client's project. |
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
`str` |
service account email address |

### list_blobs

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

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`bucket_or_name` |
`Union[ `
The bucket resource to pass or name to create. |
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
`page_size` |
`int`
(Optional) Maximum number of blobs to return in each page. Defaults to a value set by the API. |
`timeout` |
`Optional[Union[float, Tuple[float, float]]]`
The amount of time, in seconds, to wait for the server response. Can also be passed as a tuple (connect_timeout, read_timeout). See |
`retry` |
`Optional[Union[google.api_core.retry.Retry, `
How to retry the RPC. A None value will disable retries. A google.api_core.retry.Retry value will enable retries, and the object will define retriable response codes and errors and configure backoff and timeout options. A |
`match_glob` |
`str`
(Optional) A glob pattern used to filter results (for example, foo*bar). The string value must be UTF-8 encoded. See: |
`include_folders_as_prefixes` |
`bool`
(Optional) If true, includes Folders and Managed Folders in the set of |
`soft_deleted` |
`bool`
(Optional) If true, only soft-deleted objects will be listed as distinct results in order of increasing generation number. This parameter can only be used successfully if the bucket has a soft delete policy. Note |

### list_buckets

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

This will not populate the list of blobs available in each bucket.

See [API reference docs](https://cloud.google.com/storage/docs/json_api/v1/buckets/list) and a [code sample](https://cloud.google.com/storage/docs/samples/storage-list-buckets#storage_list_buckets-python).

Parameters |
|
|---|---|
Name |
Description |
`max_results` |
`int`
(Optional) The maximum number of buckets to return. |
`page_token` |
`str`
(Optional) If present, return the next batch of buckets, using the value, which must correspond to the |
`prefix` |
`str`
(Optional) Filter results to buckets whose names begin with this prefix. |
`projection` |
`str`
(Optional) Specifies the set of properties to return. If used, must be 'full' or 'noAcl'. Defaults to 'noAcl'. |
`fields` |
`str`
(Optional) Selector specifying which fields to include in a partial response. Must be a list of fields. For example to get a partial response with just the next page token and the language of each bucket returned: 'items/id,nextPageToken' |
`project` |
`str`
(Optional) The project whose buckets are to be listed. If not passed, uses the project set on the client. |
`page_size` |
`int`
(Optional) Maximum number of buckets to return in each page. Defaults to a value set by the API. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |
`soft_deleted` |
`bool`
(Optional) If true, only soft-deleted buckets will be listed as distinct results in order of increasing generation number. This parameter can only be used successfully if the bucket has a soft delete policy. See: |
`return_partial_success` |
`bool`
(Optional) If True, the response will also contain a list of unreachable buckets if the buckets are unavailable. The unreachable buckets will be available on the |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if both `project` is `None` and the client's project is also `None` . |

Returns |
|
|---|---|
Type |
Description |
|
Iterator of all
|

### list_hmac_keys

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

Parameters |
|
|---|---|
Name |
Description |
`max_results` |
`int`
(Optional) Max number of keys to return in a given page. |
`service_account_email` |
`str`
(Optional) Limit keys to those created by the given service account. |
`show_deleted_keys` |
`bool`
(Optional) Included deleted keys in the list. Default is to exclude them. |
`project_id` |
`str`
(Optional) Explicit project ID for the key. Defaults to the client's project. |
`user_project` |
`str`
(Optional) This parameter is currently ignored. |
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
`Tuple[` |
metadata for the created key, plus the bytes of the key's secret, which is an 40-character base64-encoded string. |

### lookup_bucket

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

You can use this if you would rather check for a None value than catching a NotFound exception.

Parameters |
|
|---|---|
Name |
Description |
`bucket_name` |
`str`
The name of the bucket to get. |
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

Returns |
|
|---|---|
Type |
Description |
|
The bucket matching the name provided or None if not found. |

### restore_bucket

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

Parameters |
|
|---|---|
Name |
Description |
`bucket_name` |
`str`
The name of the bucket to be restored. |
`generation` |
`int`
Selects the specific revision of the bucket. |
`projection` |
`str`
(Optional) Specifies the set of properties to return. If used, must be 'full' or 'noAcl'. Defaults to 'noAcl'. if_metageneration_match (Optional[int]): Make the operation conditional on whether the blob's current metageneration matches the given value. if_metageneration_not_match (Optional[int]): Make the operation conditional on whether the blob's current metageneration does not match the given value. |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. Users can configure non-default retry behavior. A |

Returns |
|
|---|---|
Type |
Description |
|
The restored Bucket. |

### update_user_agent

`update_user_agent(user_agent)`


Update the user-agent string for this client.

Parameter |
|
|---|---|
Name |
Description |
`user_agent` |
`str`
The string to add to the user-agent. |