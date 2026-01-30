---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.client
fetched_at: 2026-01-30T23:53:32.567314
---

# Module client (3.8.0)

Client for interacting with the Google Cloud Storage API.

## Classes

[Client](/python/docs/reference/storage/latest/google.cloud.storage.client.Client)

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

Parameters |
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