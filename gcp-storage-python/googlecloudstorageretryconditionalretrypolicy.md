---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.retry.ConditionalRetryPolicy
fetched_at: 2026-01-29T15:35:55.153912
---

# Class ConditionalRetryPolicy (3.7.0)

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

## Parameters |
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