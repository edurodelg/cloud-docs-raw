---
merged_at: 2026-01-25T15:38:56.565192
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineroutine.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine -->

# Class Routine (3.40.0)

`Routine(routine_ref, **kwargs)`


Resource representing a user-defined routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines)

## Parameters |
|
|---|---|
Name |
Description |
`routine_ref` |
`Union[str, `
A pointer to a routine. If |
|
`Dict`
Initial property values. |

## Properties

### arguments

List[[google.cloud.bigquery.routine.RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)]: Input/output
argument of a function or a stored procedure.

In-place modification is not supported. To set, replace the entire
property value with the modified list of
[RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument) objects.

### body

str: The body of the routine.

### created

Optional[datetime.datetime]: Datetime at which the routine was
created (:data:`None`

until set from the server).

Read-only.

### data_governance_type

Optional[str]: If set to `DATA_MASKING`

, the function is validated
and made available as a masking function.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not :data:`string` or :data:`None` . |

### dataset_id

str: ID of dataset containing the routine.

### description

Optional[str]: Description of the routine (defaults to
:data:`None`

).

### determinism_level

Optional[str]: (experimental) The determinism level of the JavaScript UDF if defined.

### etag

str: ETag for the resource (:data:`None`

until set from the
server).

Read-only.

### external_runtime_options

Optional[[google.cloud.bigquery.routine.ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)]:
Configures the external runtime options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### imported_libraries

List[str]: The path of the imported JavaScript libraries.

The [language](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) must
equal `JAVACRIPT`

.

Examples:
Set the `imported_libraries`

to a list of Google Cloud Storage
URIs.

```
.. code-block:: python
routine = bigquery.Routine("proj.dataset.routine_id")
routine.imported_libraries = [
"gs://cloud-samples-data/bigquery/udfs/max-value.js",
]
```


### language

Optional[str]: The language of the routine.

Defaults to `SQL`

.

### modified

Optional[datetime.datetime]: Datetime at which the routine was
last modified (:data:`None`

until set from the server).

Read-only.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### reference

[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference): Reference
describing the ID of this routine.

### remote_function_options

Optional[[google.cloud.bigquery.routine.RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)]:
Configures remote function options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### return_table_type

The return type of a Table Valued Function (TVF) routine.

.. versionadded:: 2.22.0

### return_type

google.cloud.bigquery.StandardSqlDataType: Return type of the routine.

If absent, the return type is inferred from
[body](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) at query time in
each query that references this routine. If present, then the
evaluated result will be cast to the specified returned type at query
time.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type)

### routine_id

str: The routine ID.

### type_

str: The fine-grained type of the routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType)

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.routine.routine.Routine`


Factory: construct a routine given its API representation.

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
`google.cloud.bigquery.routine.Routine` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine represented as an API resource. |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigquery_v2typesmodeldatasplitmethod_googlecloudbigquery_v2typesmo_d49d07.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodeldatasplitmethod_googlecloudbigquery_v2typesmod_3cf5a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeldatasplitmethod_googlecloudbigquery_v2typesmode_07026b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeldatasplitmethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitMethod -->

# Class DataSplitMethod (3.40.0)

`DataSplitMethod(value)`


Indicates the method to split input data into multiple tables.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelfeedbacktype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.FeedbackType -->

# Class FeedbackType (3.40.0)

`FeedbackType(value)`


Indicates the training algorithm to use for matrix factorization models.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumssqltypenames_googlecloudbigqueryquerysqlparameterscalar_b6b6ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumssqltypenames.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SqlTypeNames -->

# Class SqlTypeNames (3.40.0)

`SqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryquerysqlparameterscalartypes.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes -->

# Class SqlParameterScalarTypes (3.40.0)

`SqlParameterScalarTypes()`


Supported scalar SQL query parameter types as type objects.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodeloptimizationstrategy_googlecloudbigquery_v2typ_d87b88.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeloptimizationstrategy_googlecloudbigquery_v2type_d4a977.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeloptimizationstrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.OptimizationStrategy -->

# Class OptimizationStrategy (3.40.0)

`OptimizationStrategy(value)`


Indicates the optimization strategy used for training.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesstandardsqldatatypetypekind.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType.TypeKind -->

# Class TypeKind (3.40.0)

`TypeKind(value)`


API documentation for `bigquery_v2.types.StandardSqlDataType.TypeKind`

class.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumstimestampprecision_googlecloudbigquerydbapioperationale_b9264a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumstimestampprecision.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision -->

# Class TimestampPrecision (3.40.0)

`TimestampPrecision(value)`


Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapioperationalerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.OperationalError -->

# Class OperationalError (3.40.0)

DB-API error related to the database operation.

These errors are not necessarily under the control of the programmer.
