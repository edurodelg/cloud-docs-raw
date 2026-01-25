---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType
fetched_at: 2026-01-25T03:17:20.299216
---

# Class FieldElementType (3.40.0)


      
      Save and categorize content based on your preferences.

`FieldElementType(element_type: str)`


Represents the type of a field element.

## Parameter |
|
|---|---|
Name |
Description |
`element_type` |
`str`
The type of a field element. |

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Optional[dict],
) -> typing.Optional[google.cloud.bigquery.schema.FieldElementType]
```


Factory: construct a FieldElementType given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, str]`
field element type as returned from |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.FieldElementType` |
Python object, as parsed from `api_repr` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this field element type.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
Field element type represented as an API resource. |