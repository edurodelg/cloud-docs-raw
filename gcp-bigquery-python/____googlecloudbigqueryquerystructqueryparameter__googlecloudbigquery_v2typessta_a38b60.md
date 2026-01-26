---
merged_at: 2026-01-26T21:00:49.252960
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference -->

# Class DatasetReference (3.40.0)

`DatasetReference(project: str, dataset_id: str)`


DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

## Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
The ID of the project |
`dataset_id` |
`str`
The ID of the dataset |

## Properties

### dataset_id

str: Dataset ID.

### path

str: URL path for the dataset based on project and dataset ID.

### project

str: Project ID of the dataset.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.DatasetReference`


Factory: construct a dataset reference given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
Dataset reference resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.DatasetReference` |
Dataset reference parsed from `resource` . |

### from_string

```
from_string(
dataset_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Construct a dataset reference from dataset ID string.

Parameters |
|
|---|---|
Name |
Description |
`dataset_id` |
`str`
A dataset ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `dataset_id` is not a fully-qualified dataset ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`DatasetReference .. rubric:: Examples >>> DatasetReference.from_string('my-project-id.some_dataset') DatasetReference('my-project-id', 'some_dataset')` |
Dataset reference parsed from `dataset_id` . |

### model

`model(model_id)`


Constructs a ModelReference.

Parameter |
|
|---|---|
Name |
Description |
`model_id` |
`str`
the ID of the model. |

Returns |
|
|---|---|
Type |
Description |
|
A ModelReference for a model in this dataset. |

### routine

`routine(routine_id)`


Constructs a RoutineReference.

Parameter |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
the ID of the routine. |

Returns |
|
|---|---|
Type |
Description |
|
A RoutineReference for a routine in this dataset. |

### table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

Parameter |
|
|---|---|
Name |
Description |
`table_id` |
`str`
The ID of the table. |

Returns |
|
|---|---|
Type |
Description |
|
A table reference for a table in this dataset. |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset reference

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
dataset reference represented as an API resource |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType -->

# Class StandardSqlTableType (3.40.0)

```
StandardSqlTableType(
columns: typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField],
)
```


A table type.

## Properties

### columns

The columns in this table type.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlTableType
```


Construct an SQL table type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL table type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame -->

# Class ScriptStackFrame (3.40.0)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics -->

# Class MultiClassClassificationMetrics (3.40.0)

```
MultiClassClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Evaluation metrics for multi-class classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`confusion_matrix_list` |
`Sequence[`
Confusion matrix at different thresholds. |

## Classes

### ConfusionMatrix

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame -->

# Class ScriptStackFrame (3.40.0)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query -->

# Module query (3.40.0)

BigQuery query processing.

## Classes

[ArrayQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter)

`ArrayQueryParameter(name, array_type, values)`


Named / positional query parameters for array values.

Parameters |
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

[ArrayQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType)

`ArrayQueryParameterType(array_type, *, name=None, description=None)`


Type representation for array query parameters.

Parameters |
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

[ConnectionProperty](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty)

`ConnectionProperty(key: str = "", value: str = "")`


A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the property to set, for example, |
`value` |
`str`
The value of the property to set. |

[RangeQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter)

`RangeQueryParameter(range_element_type, start=None, end=None, name=None)`


Named / positional query parameters for range values.

Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of 'TIMESTAMP', 'DATE', or 'DATETIME'. |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`name` |
`Optional[str]`
Parameter name, used via |

[RangeQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType)

`RangeQueryParameterType(type_, *, name=None, description=None)`


Type representation for range query parameters.

Parameters |
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

[ScalarQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter)

```
ScalarQueryParameter(
name: typing.Optional[str],
type_: typing.Optional[
typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType]
],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
)
```


Named / positional query parameters for scalar values.

[ScalarQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType)

`ScalarQueryParameterType(type_, *, name=None, description=None)`


Type representation for scalar query parameters.

Parameters |
|
|---|---|
Name |
Description |
`type_` |
`str`
One of 'STRING', 'INT64', 'FLOAT64', 'NUMERIC', 'BOOL', 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[SqlParameterScalarTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes)

`SqlParameterScalarTypes()`


Supported scalar SQL query parameter types as type objects.

[StructQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter)

`StructQueryParameter(name, *sub_params)`


Name / positional query parameters for struct values.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |

[StructQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType)

`StructQueryParameterType(*fields, name=None, description=None)`


Type representation for struct query parameters.

Parameters |
|
|---|---|
Name |
Description |
`fields` |
`Iterable[Union[ ArrayQueryParameterType, ScalarQueryParameterType, StructQueryParameterType ]]`
An non-empty iterable describing the struct's field types. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[UDFResource](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource)

`UDFResource(udf_type, value)`


Describe a single user-defined function (UDF) resource.

Parameters |
|
|---|---|
Name |
Description |
`udf_type` |
`str`
The type of the resource ('inlineCode' or 'resourceUri') |
`value` |
`str See: https://cloud.google.com/bigquery/user-defined-functions#api`
The inline code or resource URI. |
