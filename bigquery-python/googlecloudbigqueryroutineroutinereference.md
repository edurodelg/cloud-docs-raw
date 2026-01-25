---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference
fetched_at: 2026-01-25T02:10:55.581538
---

# Class RoutineReference (3.40.0)


      
      Save and categorize content based on your preferences.

`RoutineReference()`


A pointer to a routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference)

## Properties

### dataset_id

str: ID of dataset containing the routine.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### routine_id

str: The routine ID.

## Methods

### __eq__

`__eq__(other)`


Two RoutineReferences are equal if they point to the same routine.

### __str__

`__str__()`


String representation of the reference.

This is a fully-qualified ID, including the project ID and dataset ID.

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Routine reference representation returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `resource` . |

### from_string

```
from_string(
routine_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference from routine ID string.

Parameters |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
A routine ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `routine_id` is not a fully-qualified routine ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `routine_id` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine reference.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine reference represented as an API resource. |