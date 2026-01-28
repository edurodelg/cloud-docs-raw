---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.hmac_key
fetched_at: 2026-01-28T07:26:16.757682
---

# Module hmac_key (3.7.0)

Configure HMAC keys that can be used to authenticate requests to Google Cloud Storage.

## Classes

[HMACKeyMetadata](/python/docs/reference/storage/latest/google.cloud.storage.hmac_key.HMACKeyMetadata)

`HMACKeyMetadata(client, access_id=None, project_id=None, user_project=None)`


Metadata about an HMAC service account key withn Cloud Storage.

Parameters |
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