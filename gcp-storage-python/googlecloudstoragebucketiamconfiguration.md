---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.IAMConfiguration
fetched_at: 2026-02-08T01:08:19.301122
---

# Class IAMConfiguration (3.8.0)

```
IAMConfiguration(
bucket,
public_access_prevention=object,
uniform_bucket_level_access_enabled=object,
uniform_bucket_level_access_locked_time=object,
bucket_policy_only_enabled=object,
bucket_policy_only_locked_time=object,
)
```


Map a bucket's IAM configuration.

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

### bucket_policy_only_enabled

Deprecated alias for `uniform_bucket_level_access_enabled`

.

Returns |
|
|---|---|
Type |
Description |
`bool` |
whether the bucket is configured to allow only IAM. |

### bucket_policy_only_locked_time

Deprecated alias for `uniform_bucket_level_access_locked_time`

.

Returns |
|
|---|---|
Type |
Description |
`Union[` |
(readonly) Time after which `bucket_policy_only_enabled` will be frozen as true. |

### public_access_prevention

Setting for public access prevention policy. Options are 'inherited' (default) or 'enforced'.

```
See: https://cloud.google.com/storage/docs/public-access-prevention
```


Returns |
|
|---|---|
Type |
Description |
`string` |
the public access prevention status, either 'enforced' or 'inherited'. |

### uniform_bucket_level_access_enabled

If set, access checks only use bucket-level IAM policies or above.

Returns |
|
|---|---|
Type |
Description |
`bool` |
whether the bucket is configured to allow only IAM. |

### uniform_bucket_level_access_locked_time

Deadline for changing `uniform_bucket_level_access_enabled`

from true to false.

If the bucket's `uniform_bucket_level_access_enabled`

is true, this property
is time time after which that setting becomes immutable.

If the bucket's `uniform_bucket_level_access_enabled`

is false, this property
is `None`

.

Returns |
|
|---|---|
Type |
Description |
`Union[` |
(readonly) Time after which `uniform_bucket_level_access_enabled` will be frozen as true. |

## Methods

### clear

`clear()`


API documentation for `storage.bucket.IAMConfiguration.clear`

method.

### copy

`copy()`


API documentation for `storage.bucket.IAMConfiguration.copy`

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


API documentation for `storage.bucket.IAMConfiguration.items`

method.

### keys

`keys()`


API documentation for `storage.bucket.IAMConfiguration.keys`

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


API documentation for `storage.bucket.IAMConfiguration.values`

method.