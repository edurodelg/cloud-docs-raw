---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType
fetched_at: 2026-01-25T02:10:22.439248
---

# Class RangeQueryParameterType (3.40.0)


      
      Save and categorize content based on your preferences.

`RangeQueryParameterType(type_, *, name=None, description=None)`


Type representation for range query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Union[ScalarQueryParameterType, str]`
Type of range element, must be one of 'TIMESTAMP', 'DATETIME', or 'DATE'. |
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
`google.cloud.bigquery.query.RangeQueryParameterType` |
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

### with_name

`with_name(new_name: typing.Optional[str])`


Return a copy of the instance with `name`

set to `new_name`

.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Union[str, None]`
The new name of the range query parameter type. If |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameterType` |
A new instance with updated name. |