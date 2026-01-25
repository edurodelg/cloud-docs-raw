---
merged_at: 2026-01-25T15:38:56.567094
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryquerystructqueryparameter__googlecloudbigquery_v2typesstand_d4ab27.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryquerystructqueryparameter__googlecloudbigquery_v2typesstanda_78aef6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryquerystructqueryparameter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter -->

# Class StructQueryParameter (3.40.0)

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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesstandardsqltabletype_googlecloudbigqueryjobcreatedis_495b17.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesstandardsqltabletype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType -->

# Class StandardSqlTableType (3.40.0)

`StandardSqlTableType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A table type

## Attribute |
|
|---|---|
Name |
Description |
`columns` |
`Sequence[`
The columns in this table type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobcreatedisposition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition -->

# Class CreateDisposition (3.40.0)

`CreateDisposition()`


Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineexternalruntimeoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions -->

# Class ExternalRuntimeOptions (3.40.0)

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


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryenumscreatedisposition_googlecloudbigqueryjoboperationtype_d6a996.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumscreatedisposition_googlecloudbigqueryjoboperationtype__6a50d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumscreatedisposition_googlecloudbigqueryjoboperationtype.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumscreatedisposition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition -->

# Class CreateDisposition (3.40.0)

`CreateDisposition()`


Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjoboperationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.OperationType -->

# Class OperationType (3.40.0)

`OperationType()`


Different operation types supported in table copy job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelclusteringmetricscluster.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster -->

# Class Cluster (3.40.0)

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`feature_values` |
`Sequence[`
Values of highly variant features for this cluster. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
Count of training data rows that were assigned to this cluster. |

## Classes

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a single feature within the cluster.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryroutineroutinetype_googlecloudbigqueryenumssourcecolumnmatc_93b0a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryroutineroutinetype_googlecloudbigqueryenumssourcecolumnmatch.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineroutinetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineType -->

# Class RoutineType (3.40.0)

`RoutineType()`


The fine-grained type of the routine.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype)

.. versionadded:: 2.22.0


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumssourcecolumnmatch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch -->

# Class SourceColumnMatch (3.40.0)

`SourceColumnMatch(value)`


Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryarrayqueryparametertype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType -->

# Class ArrayQueryParameterType (3.40.0)

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
