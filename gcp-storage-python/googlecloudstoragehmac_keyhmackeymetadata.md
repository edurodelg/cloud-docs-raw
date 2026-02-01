---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata
fetched_at: 2026-02-01T07:58:49.360419
---

# Class HMACKeyMetadata (3.8.0)

`HMACKeyMetadata(client, access_id=None, project_id=None, user_project=None)`


Metadata about an HMAC service account key withn Cloud Storage.

## Parameters |
|
|---|---|
Name |
Description |
`client` |
`Client`
client associated with the key metadata. |
`access_id` |
`str`
(Optional) Unique ID of an existing key. |
`project_id` |
`str`
(Optional) Project ID of an existing key. Defaults to client's project. |
`user_project` |
`str`
(Optional) This parameter is currently ignored. |

## Properties

### access_id

Access ID of the key.

Returns |
|
|---|---|
Type |
Description |
`str or None` |
unique identifier of the key within a project. |

### etag

ETag identifying the version of the key metadata.

Returns |
|
|---|---|
Type |
Description |
`str or None` |
ETag for the version of the key's metadata. |

### id

ID of the key, including the Project ID and the Access ID.

Returns |
|
|---|---|
Type |
Description |
`str or None` |
ID of the key. |

### path

Resource path for the metadata's key.

### project

Project ID associated with the key.

Returns |
|
|---|---|
Type |
Description |
`str or None` |
project identfier for the key. |

### service_account_email

Service account e-mail address associated with the key.

Returns |
|
|---|---|
Type |
Description |
`str or None` |
e-mail address for the service account which created the key. |

### state

Get / set key's state.

One of:

`ACTIVE`

`INACTIVE`

`DELETED`


Returns |
|
|---|---|
Type |
Description |
`str or None` |
key's current state. |

### time_created

Retrieve the timestamp at which the HMAC key was created.

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the bucket's resource has not been loaded from the server. |

### updated

Retrieve the timestamp at which the HMAC key was created.

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the bucket's resource has not been loaded from the server. |

### user_project

Project ID to be billed for API requests made via this bucket.

This property is currently ignored by the server.

## Methods

### delete

`delete(timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Delete the key from Cloud Storage.

Parameters |
|
|---|---|
Name |
Description |
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
|
if the key does not exist on the back-end. |

### exists

`exists(timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Determine whether or not the key for this metadata exists.

Parameters |
|
|---|---|
Name |
Description |
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
`bool` |
True if the key exists in Cloud Storage. |

### reload

`reload(timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Reload properties from Cloud Storage.

Parameters |
|
|---|---|
Name |
Description |
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
|
if the key does not exist on the back-end. |

### update

`update(timeout=60, retry=google.cloud.storage.retry.ConditionalRetryPolicy)`


Save writable properties to Cloud Storage.

Parameters |
|
|---|---|
Name |
Description |
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
|
if the key does not exist on the back-end. |