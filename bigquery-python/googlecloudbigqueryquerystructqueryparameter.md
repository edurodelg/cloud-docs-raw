---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter
fetched_at: 2026-01-25T02:10:32.044348
---

# Class StructQueryParameter (3.40.0)


      
      Save and categorize content based on your preferences.

`StructQueryParameter(name, *sub_params)`


Name / positional query parameters for struct values.

## Parameter |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.StructQueryParameter`


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
`google.cloud.bigquery.query.StructQueryParameter` |
Instance |

### positional

`positional(*sub_params)`


Factory for positional parameters.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.StructQueryParameter` |
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