---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions
fetched_at: 2026-01-25T02:10:46.341634
---

# Class ExternalRuntimeOptions (3.40.0)


      
      Save and categorize content based on your preferences.

```
ExternalRuntimeOptions(
container_memory: typing.Optional[str] = None,
container_cpu: typing.Optional[int] = None,
runtime_connection: typing.Optional[str] = None,
max_batching_rows: typing.Optional[int] = None,
runtime_version: typing.Optional[str] = None,
_properties: typing.Optional[typing.Dict] = None,
)
```


Options for the runtime of the external system.

## Parameters |
|
|---|---|
Name |
Description |
`container_memory` |
`str`
Optional. Amount of memory provisioned for a Python UDF container instance. Format: {number}{unit} where unit is one of "M", "G", "Mi" and "Gi" (e.g. 1G, 512Mi). If not specified, the default value is 512Mi. For more information, see |
`container_cpu` |
`int`
Optional. Amount of CPU provisioned for a Python UDF container instance. For more information, see |
`runtime_connection` |
`str`
Optional. Fully qualified name of the connection whose service account will be used to execute the code in the container. Format: "projects/{projectId}/locations/{locationId}/connections/{connectionId}" |
`max_batching_rows` |
`int`
Optional. Maximum number of rows in each batch sent to the external runtime. If absent or if 0, BigQuery dynamically decides the number of rows in a batch. |
`runtime_version` |
`str`
Optional. Language runtime version. Example: python-3.11. |

## Properties

### container_cpu

Optional. Amount of CPU provisioned for a Python UDF container instance.

### container_memory

Optional. Amount of memory provisioned for a Python UDF container instance.

### max_batching_rows

Optional. Maximum number of rows in each batch sent to the external runtime.

### runtime_connection

Optional. Fully qualified name of the connection.

### runtime_version

Optional. Language runtime version.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.ExternalRuntimeOptions
```


Factory: construct external runtime options given its API representation.

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
`google.cloud.bigquery.routine.ExternalRuntimeOptions` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this ExternalRuntimeOptions.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
External runtime options represented as an API resource. |