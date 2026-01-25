---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo
fetched_at: 2026-01-25T02:11:05.045145
---

# Class ForeignTypeInfo (3.40.0)


      
      Save and categorize content based on your preferences.

`ForeignTypeInfo(type_system: typing.Optional[str] = None)`


Metadata about the foreign data type definition such as the system in which the type is defined.

## Parameter |
|
|---|---|
Name |
Description |
`type_system` |
`str`
Required. Specifies the system which defines the foreign data type. TypeSystem enum currently includes: * "TYPE_SYSTEM_UNSPECIFIED" * "HIVE" |

## Properties

### type_system

Required. Specifies the system which defines the foreign data type.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.schema.ForeignTypeInfo
```


Factory: constructs an instance of the class (cls) given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, Any]`
API representation of the object to be instantiated. |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, Any]` |
A dictionary in the format used by the BigQuery API. |