---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification
fetched_at: 2026-01-30T23:54:04.020146
---

# Module notification (3.8.0)

Configure bucket notification resources to interact with Google Cloud Pub/Sub.

## Classes

[BucketNotification](/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification)

```
BucketNotification(
bucket,
topic_name=None,
topic_project=None,
custom_attributes=None,
event_types=None,
blob_name_prefix=None,
payload_format="NONE",
notification_id=None,
)
```


Represent a single notification resource for a bucket.

See: [https://cloud.google.com/storage/docs/json_api/v1/notifications](https://cloud.google.com/storage/docs/json_api/v1/notifications)

Parameters |
|
|---|---|
Name |
Description |
`bucket` |
Bucket to which the notification is bound. |
`topic_name` |
`str`
(Optional) Topic name to which notifications are published. |
`topic_project` |
`str`
(Optional) Project ID of topic to which notifications are published. If not passed, uses the project ID of the bucket's client. |
`custom_attributes` |
`dict`
(Optional) Additional attributes passed with notification events. |
`event_types` |
`list(str)`
(Optional) Event types for which notification events are published. |
`blob_name_prefix` |
`str`
(Optional) Prefix of blob names for which notification events are published. |
`payload_format` |
`str`
(Optional) Format of payload for notification events. |
`notification_id` |
`str`
(Optional) The ID of the notification. |