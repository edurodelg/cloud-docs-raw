---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType
fetched_at: 2026-01-25T02:10:09.213993
---

# Class ArrayQueryParameterType (3.40.0)


      
      Save and categorize content based on your preferences.

`ArrayQueryParameterType(array_type, *, name=None, description=None)`


Type representation for array query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ArrayQueryParameterType` |
Instance |

### to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |