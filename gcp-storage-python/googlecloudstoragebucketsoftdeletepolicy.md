---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.SoftDeletePolicy
fetched_at: 2026-01-28T07:25:47.698359
---

# Class SoftDeletePolicy (3.7.0)

`SoftDeletePolicy(bucket, **kw)`


Map a bucket's soft delete policy.

## Parameters |
|
|---|---|
Name |
Description |
`bucket` |
Bucket for which this instance is the policy. |
`retention_duration_seconds` |
`int`
(Optional) The period of time in seconds that soft-deleted objects in the bucket will be retained and cannot be permanently deleted. |
`effective_time` |
(Optional) When the bucket's soft delete policy is effective. This value should normally only be set by the back-end API. |

## Properties

### bucket

Bucket for which this instance is the policy.

Returns |
|
|---|---|
Type |
Description |
|
the instance's bucket. |

### effective_time

Get the effective time of the bucket's soft delete policy.

Returns |
|
|---|---|
Type |
Description |
`datetime.datetime or ` |
point-in time at which the bucket's soft delte policy is effective, or `None` if the property is not set. |

### retention_duration_seconds

Get the retention duration of the bucket's soft delete policy.

Returns |
|
|---|---|
Type |
Description |
`int or ` |
The period of time in seconds that soft-deleted objects in the bucket will be retained and cannot be permanently deleted; Or `None` if the property is not set. |

## Methods

### clear

`clear()`


API documentation for `storage.bucket.SoftDeletePolicy.clear`

method.

### copy

`copy()`


API documentation for `storage.bucket.SoftDeletePolicy.copy`

method.

### from_api_repr

`from_api_repr(resource, bucket)`


Factory: construct instance from resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`dict`
mapping as returned from API call. |

Returns |
|
|---|---|
Type |
Description |
|
Instance created from resource. |

### fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

### get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

### items

`items()`


API documentation for `storage.bucket.SoftDeletePolicy.items`

method.

### keys

`keys()`


API documentation for `storage.bucket.SoftDeletePolicy.keys`

method.

### pop

`pop(k[,d])`


If the key is not found, return the default if given; otherwise, raise a KeyError.

### popitem

`popitem()`


Remove and return a (key, value) pair as a 2-tuple.

Pairs are returned in LIFO (last-in, first-out) order. Raises KeyError if the dict is empty.

### setdefault

`setdefault(key, default=None, /)`


Insert key with a value of default if key is not in the dictionary.

Return the value for key if key is in the dictionary, else default.

### update

`update([E, ]**F)`


If E is present and has a .keys() method, then does: for k in E: D[k] = E[k] If E is present and lacks a .keys() method, then does: for k, v in E: D[k] = v In either case, this is followed by: for k in F: D[k] = F[k]

### values

`values()`


API documentation for `storage.bucket.SoftDeletePolicy.values`

method.