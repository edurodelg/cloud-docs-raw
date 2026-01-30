---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.retry
fetched_at: 2026-01-30T23:54:08.353551
---

# Module retry (3.8.0)

Helpers for configuring retries with exponential back-off.

## Classes

[ConditionalRetryPolicy](/python/docs/reference/storage/latest/google.cloud.storage.retry.ConditionalRetryPolicy)

`ConditionalRetryPolicy(retry_policy, conditional_predicate, required_kwargs)`


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

Parameters |
|
|---|---|
Name |
Description |
`retry_policy` |
`class:`
A retry object defining timeouts, persistence and which exceptions to retry. |
`conditional_predicate` |
`callable`
A callable that accepts exactly the number of arguments in |
`required_kwargs` |
`list(str)`
A list of keyword argument keys that will be extracted from the API call and passed into the |

## Modules Functions

### is_etag_in_data

`is_etag_in_data(data)`


Return True if an etag is contained in the request body.

Parameter |
|
|---|---|
Name |
Description |
`data` |
`dict or None`
A dict representing the request JSON body. If not passed, returns False. |

### is_etag_in_json

`is_etag_in_json(data)`


`is_etag_in_json`

is supported for backwards-compatibility reasons only;
please use `is_etag_in_data`

instead.

### is_generation_specified

`is_generation_specified(query_params)`


Return True if generation or if_generation_match is specified.

### is_metageneration_specified

`is_metageneration_specified(query_params)`


Return True if if_metageneration_match is specified.