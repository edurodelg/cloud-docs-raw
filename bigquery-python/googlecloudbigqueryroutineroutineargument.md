---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument
fetched_at: 2026-01-25T02:10:53.227838
---

# Class RoutineArgument (3.40.0)


      
      Save and categorize content based on your preferences.

`RoutineArgument(**kwargs)`


Input/output argument of a function or a stored procedure.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument)

## Parameter |
|
|---|---|
Name |
Description |
|
`Dict`
Initial property values. |

## Properties

### data_type

Optional[google.cloud.bigquery.StandardSqlDataType]: Type of a variable, e.g., a function argument.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.data_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.data_type)

### kind

Optional[str]: The kind of argument, for example `FIXED_TYPE`

or
`ANY_TYPE`

.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.argument_kind](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.argument_kind)

### mode

Optional[str]: The input/output mode of the argument.

### name

Optional[str]: Name of this argument.

Can be absent for function return argument.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineArgument
```


Factory: construct a routine argument given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Resource, as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineArgument` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine argument.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine argument represented as an API resource. |