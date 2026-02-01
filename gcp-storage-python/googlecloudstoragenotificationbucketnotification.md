---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.notification.BucketNotification
fetched_at: 2026-02-01T07:58:54.702807
---

# Class BucketNotification (3.8.0)

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

## Parameters |
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

## Properties

### blob_name_prefix

Prefix of blob names for which notification events are published.

### bucket

Bucket to which the notification is bound.

### client

The client bound to this notfication.

### custom_attributes

Custom attributes passed with notification events.

### etag

Server-set ETag of notification resource.

### event_types

Event types for which notification events are published.

### notification_id

Server-set ID of notification resource.

### path

The URL path for this notification.

### payload_format

Format of payload of notification events.

### self_link

Server-set ETag of notification resource.

### topic_name

Topic name to which notifications are published.

### topic_project

Project ID of topic to which notifications are published.

## Methods

### create

`create(client=None, timeout=60, retry=None)`


API wrapper: create the notification.

See:
[https://cloud.google.com/storage/docs/json_api/v1/notifications/insert](https://cloud.google.com/storage/docs/json_api/v1/notifications/insert)

If `user_project`

is set on the bucket, bills the API request
to that project.

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
if the notification already exists. |

### delete

`delete(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Delete this notification.

See:
[https://cloud.google.com/storage/docs/json_api/v1/notifications/delete](https://cloud.google.com/storage/docs/json_api/v1/notifications/delete)

If `user_project`

is set on the bucket, bills the API request
to that project.

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
|
if the notification does not exist. |
`ValueError` |
if the notification has no ID. |

### exists

`exists(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Test whether this notification exists.

See:
[https://cloud.google.com/storage/docs/json_api/v1/notifications/get](https://cloud.google.com/storage/docs/json_api/v1/notifications/get)

If `user_project`

is set on the bucket, bills the API request
to that project.

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
if the notification has no ID. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True, if the notification exists, else False. |

### from_api_repr

`from_api_repr(resource, bucket)`


Construct an instance from the JSON repr returned by the server.

See: [https://cloud.google.com/storage/docs/json_api/v1/notifications](https://cloud.google.com/storage/docs/json_api/v1/notifications)

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`dict`
JSON repr of the notification |
`bucket` |
Bucket to which the notification is bound. |

Returns |
|
|---|---|
Type |
Description |
|
the new notification instance |

### reload

`reload(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Update this notification from the server configuration.

See:
[https://cloud.google.com/storage/docs/json_api/v1/notifications/get](https://cloud.google.com/storage/docs/json_api/v1/notifications/get)

If `user_project`

is set on the bucket, bills the API request
to that project.

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
if the notification has no ID. |