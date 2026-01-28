---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.acl.ACL
fetched_at: 2026-01-28T07:25:01.767035
---

# Class ACL (3.7.0)

`ACL()`


Container class representing a list of access controls.

## Properties

### client

Abstract getter for the object client.

## Methods

### add_entity

`add_entity(entity)`


Add an entity to the ACL.

Parameter |
|
|---|---|
Name |
Description |
`entity` |
The entity to add to this ACL. |

### all

`all()`


Factory method for an Entity representing all users.

Returns |
|
|---|---|
Type |
Description |
|
An entity representing all users. |

### all_authenticated

`all_authenticated()`


Factory method for an Entity representing all authenticated users.

Returns |
|
|---|---|
Type |
Description |
|
An entity representing all authenticated users. |

### clear

```
clear(
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Remove all ACL entries.

If `user_project`

is set, bills the API request to that project.

Note that this won't actually remove *ALL* the rules, but it
will remove all the non-default rules. In short, you'll still
have access to a bucket that you created even after you clear
ACL rules with this method.

Parameters |
|
|---|---|
Name |
Description |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

### domain

`domain(domain)`


Factory method for a domain Entity.

Parameter |
|
|---|---|
Name |
Description |
`domain` |
`str`
The domain for this entity. |

Returns |
|
|---|---|
Type |
Description |
|
An entity corresponding to this domain. |

### entity

`entity(entity_type, identifier=None)`


Factory method for creating an Entity.

If an entity with the same type and identifier already exists, this will return a reference to that entity. If not, it will create a new one and add it to the list of known entities for this ACL.

Parameters |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
The type of entity to create (ie, |
`identifier` |
`str`
The ID of the entity (if applicable). This can be either an ID or an e-mail address. |

Returns |
|
|---|---|
Type |
Description |
|
A new Entity or a reference to an existing identical entity. |

### entity_from_dict

`entity_from_dict(entity_dict)`


Build an _ACLEntity object from a dictionary of data.

An entity is a mutable object that represents a list of roles belonging to either a user or group or the special types for all users and all authenticated users.

Parameter |
|
|---|---|
Name |
Description |
`entity_dict` |
`dict`
Dictionary full of data from an ACL lookup. |

Returns |
|
|---|---|
Type |
Description |
|
An Entity constructed from the dictionary. |

### get_entities

`get_entities()`


Get a list of all Entity objects.

Returns |
|
|---|---|
Type |
Description |
`list of ` |
A list of all Entity objects. |

### get_entity

`get_entity(entity, default=None)`


Gets an entity object from the ACL.

Parameters |
|
|---|---|
Name |
Description |
`entity` |
The entity to get lookup in the ACL. |
`default` |
`anything`
This value will be returned if the entity doesn't exist. |

Returns |
|
|---|---|
Type |
Description |
|
The corresponding entity or the value provided to `default` . |

### group

`group(identifier)`


Factory method for a group Entity.

Parameter |
|
|---|---|
Name |
Description |
`identifier` |
`str`
An id or e-mail for this particular group. |

Returns |
|
|---|---|
Type |
Description |
|
An Entity corresponding to this group. |

### has_entity

`has_entity(entity)`


Returns whether or not this ACL has any entries for an entity.

Parameter |
|
|---|---|
Name |
Description |
`entity` |
The entity to check for existence in this ACL. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True of the entity exists in the ACL. |

### reload

`reload(client=None, timeout=60, retry=google.api_core.retry.retry_unary.Retry)`


Reload the ACL data from Cloud Storage.

If `user_project`

is set, bills the API request to that project.

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
(Optional) How to retry the RPC. See: |

### reset

`reset()`


Remove all entities from the ACL, and clear the `loaded`

flag.

### save

```
save(
acl=None,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Save this ACL for the current bucket.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`acl` |
The ACL object to save. If left blank, this will save current entries. |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

### save_predefined

```
save_predefined(
predefined,
client=None,
if_generation_match=None,
if_generation_not_match=None,
if_metageneration_match=None,
if_metageneration_not_match=None,
timeout=60,
retry=google.cloud.storage.retry.ConditionalRetryPolicy,
)
```


Save this ACL for the current bucket using a predefined ACL.

If `user_project`

is set, bills the API request to that project.

Parameters |
|
|---|---|
Name |
Description |
`predefined` |
`str`
An identifier for a predefined ACL. Must be one of the keys in |
`client` |
(Optional) The client to use. If not passed, falls back to the |
`if_generation_match` |
`long`
(Optional) See :ref: |
`if_generation_not_match` |
`long`
(Optional) See :ref: |
`if_metageneration_match` |
`long`
(Optional) See :ref: |
`if_metageneration_not_match` |
`long`
(Optional) See :ref: |
`timeout` |
`float or tuple`
(Optional) The amount of time, in seconds, to wait for the server response. See: |
`retry` |
`google.api_core.retry.Retry or `
(Optional) How to retry the RPC. See: |

### user

`user(identifier)`


Factory method for a user Entity.

Parameter |
|
|---|---|
Name |
Description |
`identifier` |
`str`
An id or e-mail for this particular user. |

Returns |
|
|---|---|
Type |
Description |
|
An Entity corresponding to this user. |

### validate_predefined

`validate_predefined(predefined)`


Ensures predefined is in list of predefined json values

Parameter |
|
|---|---|
Name |
Description |
`predefined` |
`str`
validated JSON name of predefined acl |

Exceptions |
|
|---|---|
Type |
Description |
`:exc` |
`ValueError` : If predefined is not a valid acl |