---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.bucket.LifecycleRuleConditions
fetched_at: 2026-02-02T16:07:15.462130
---

# Class LifecycleRuleConditions (3.8.0)

```
LifecycleRuleConditions(
age=None,
created_before=None,
is_live=None,
matches_storage_class=None,
number_of_newer_versions=None,
days_since_custom_time=None,
custom_time_before=None,
days_since_noncurrent_time=None,
noncurrent_time_before=None,
matches_prefix=None,
matches_suffix=None,
_factory=False,
)
```


Map a single lifecycle rule for a bucket.

## Parameters |
|
|---|---|
Name |
Description |
`age` |
`int`
(Optional) Apply rule action to items whose age, in days, exceeds this value. |
`created_before` |
`datetime.date`
(Optional) Apply rule action to items created before this date. |
`is_live` |
`bool`
(Optional) If true, apply rule action to non-versioned items, or to items with no newer versions. If false, apply rule action to versioned items with at least one newer version. |
`matches_prefix` |
`list(str)`
(Optional) Apply rule action to items which any prefix matches the beginning of the item name. |
`matches_storage_class` |
`list(str), one or more of `
(Optional) Apply rule action to items whose storage class matches this value. |
`matches_suffix` |
`list(str)`
(Optional) Apply rule action to items which any suffix matches the end of the item name. |
`number_of_newer_versions` |
`int`
(Optional) Apply rule action to versioned items having N newer versions. |
`days_since_custom_time` |
`int`
(Optional) Apply rule action to items whose number of days elapsed since the custom timestamp. This condition is relevant only for versioned objects. The value of the field must be a non negative integer. If it's zero, the object version will become eligible for lifecycle action as soon as it becomes custom. |
`custom_time_before` |
(Optional) Date object parsed from RFC3339 valid date, apply rule action to items whose custom time is before this date. This condition is relevant only for versioned objects, e.g., 2019-03-16. |
`days_since_noncurrent_time` |
`int`
(Optional) Apply rule action to items whose number of days elapsed since the non current timestamp. This condition is relevant only for versioned objects. The value of the field must be a non negative integer. If it's zero, the object version will become eligible for lifecycle action as soon as it becomes non current. |
`noncurrent_time_before` |
(Optional) Date object parsed from RFC3339 valid date, apply rule action to items whose non current time is before this date. This condition is relevant only for versioned objects, e.g, 2019-03-16. |

## Properties

### age

Conditon's age value.

### created_before

Conditon's created_before value.

### custom_time_before

Conditon's 'custom_time_before' value.

### days_since_custom_time

Conditon's 'days_since_custom_time' value.

### days_since_noncurrent_time

Conditon's 'days_since_noncurrent_time' value.

### is_live

Conditon's 'is_live' value.

### matches_prefix

Conditon's 'matches_prefix' value.

### matches_storage_class

Conditon's 'matches_storage_class' value.

### matches_suffix

Conditon's 'matches_suffix' value.

### noncurrent_time_before

Conditon's 'noncurrent_time_before' value.

### number_of_newer_versions

Conditon's 'number_of_newer_versions' value.

## Methods

### clear

`clear()`


API documentation for `storage.bucket.LifecycleRuleConditions.clear`

method.

### copy

`copy()`


API documentation for `storage.bucket.LifecycleRuleConditions.copy`

method.

### from_api_repr

`from_api_repr(resource)`


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


API documentation for `storage.bucket.LifecycleRuleConditions.items`

method.

### keys

`keys()`


API documentation for `storage.bucket.LifecycleRuleConditions.keys`

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


API documentation for `storage.bucket.LifecycleRuleConditions.values`

method.