---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.blob.Retention
fetched_at: 2026-01-29T15:34:47.174752
---

# Class Retention (3.7.0)

`Retention(blob, mode=None, retain_until_time=None, retention_expiration_time=None)`


Map an object's retention configuration.

## Properties

### blob

Blob for which this retention configuration applies to.

Returns |
|
|---|---|
Type |
Description |
|
the instance's blob. |

### mode

The mode of the retention configuration. Options are 'Unlocked' or 'Locked'.

Returns |
|
|---|---|
Type |
Description |
`string` |
The mode of the retention configuration, which can be either set to 'Unlocked' or 'Locked'. |

### retain_until_time

The earliest time that the object can be deleted or replaced, which is the retention configuration set for this object.

Returns |
|
|---|---|
Type |
Description |
|
Datetime object parsed from RFC3339 valid timestamp, or `None` if the blob's resource has not been loaded from the server (see `reload` ). |

### retention_expiration_time

The earliest time that the object can be deleted, which depends on any retention configuration set for the object and any retention policy set for the bucket that contains the object.

Returns |
|
|---|---|
Type |
Description |
|
(readonly) The earliest time that the object can be deleted. |

## Methods

### clear

`clear()`


API documentation for `storage.blob.Retention.clear`

method.

### copy

`copy()`


API documentation for `storage.blob.Retention.copy`

method.

### from_api_repr

`from_api_repr(resource, blob)`


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
Retention configuration created from resource. |

### fromkeys

`fromkeys(value=None, /)`


Create a new dictionary with keys from iterable and values set to value.

### get

`get(key, default=None, /)`


Return the value for key if key is in the dictionary, else default.

### items

`items()`


API documentation for `storage.blob.Retention.items`

method.

### keys

`keys()`


API documentation for `storage.blob.Retention.keys`

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


API documentation for `storage.blob.Retention.values`

method.