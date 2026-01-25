---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList
fetched_at: 2026-01-25T03:17:25.611265
---

# Class PolicyTagList (3.40.0)


      
      Save and categorize content based on your preferences.

`PolicyTagList(names: typing.Iterable[str] = ())`


Define Policy Tags for a column.

## Properties

### names

Tuple[str]: Policy tags associated with this definition.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.PolicyTagList`


Return a `PolicyTagList`

object deserialized from a dict.

This method creates a new `PolicyTagList`

instance that points to
the `api_repr`

parameter as its internal properties dict. This means
that when a `PolicyTagList`

instance is stored as a property of
another object, any changes made at the higher level will also appear
here.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Mapping[str, str]`
The serialized representation of the PolicyTagList, such as what is output by |

Returns |
|
|---|---|
Type |
Description |
`Optional[google.cloud.bigquery.schema.PolicyTagList]` |
The `PolicyTagList` object or None. |

### to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

This method returns the properties dict of the `PolicyTagList`

instance rather than making a copy. This means that when a
`PolicyTagList`

instance is stored as a property of another
object, any changes made at the higher level will also appear here.

Returns |
|
|---|---|
Type |
Description |
`dict` |
A dictionary representing the PolicyTagList object in serialized form. |