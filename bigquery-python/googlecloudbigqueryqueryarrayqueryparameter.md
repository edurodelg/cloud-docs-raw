---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter
fetched_at: 2026-01-25T03:16:22.906364
---

# Class ArrayQueryParameter (3.40.0)


      
      Save and categorize content based on your preferences.

`ArrayQueryParameter(name, array_type, values)`


Named / positional query parameters for array values.

## Parameters |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ArrayQueryParameter`


Factory: construct parameter from JSON resource.

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
`google.cloud.bigquery.query.ArrayQueryParameter` |
Instance |

### positional

```
positional(
array_type: str, values: list
) -> google.cloud.bigquery.query.ArrayQueryParameter
```


Factory for positional parameters.

Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ArrayQueryParameter` |
Instance without name |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |