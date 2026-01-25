---
merged_at: 2026-01-25T15:38:56.571458
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenums.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums -->

# Module enums (3.40.0)

API documentation for `bigquery.enums`

module.

## Classes

[AutoRowIDs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.AutoRowIDs)

`AutoRowIDs(value)`


How to handle automatic insert IDs when inserting rows as a stream.

[BigLakeFileFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat)

`BigLakeFileFormat()`


API documentation for `bigquery.enums.BigLakeFileFormat`

class.

[BigLakeTableFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat)

`BigLakeTableFormat()`


API documentation for `bigquery.enums.BigLakeTableFormat`

class.

[Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

[CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition)

`CreateDisposition()`


Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

[DatasetView](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DatasetView)

`DatasetView(value)`


DatasetView specifies which dataset information is returned.

[DecimalTargetType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType)

`DecimalTargetType()`


The data types that could be used as a target type when converting decimal values.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType)

.. versionadded:: 2.21.0

[DefaultPandasDTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes)

`DefaultPandasDTypes(value)`


Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)

[DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

[DeterminismLevel](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

[Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Encoding)

`Encoding()`


The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

[EntityTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.EntityTypes)

`EntityTypes(value)`


Enum of allowed entity type names in AccessEntry

[JobCreationMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode)

`JobCreationMode()`


Documented values for Job Creation Mode.

[KeyResultStatementKind](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.KeyResultStatementKind)

`KeyResultStatementKind()`


Determines which statement in the script represents the "key result".

The "key result" is used to populate the schema and query results of the script job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind)

[QueryApiMethod](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryApiMethod)

`QueryApiMethod(value)`


API method used to start the query. The default value is
`INSERT`

.

[QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryPriority)

`QueryPriority()`


Specifies a priority for the query. The default value is
`INTERACTIVE`

.

[RoundingMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.RoundingMode)

`RoundingMode(value)`


Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

ROUNDING_MODE_UNSPECIFIED: will default to using ROUND_HALF_AWAY_FROM_ZERO.

ROUND_HALF_AWAY_FROM_ZERO: rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5, 1.6, 1.7, 1.8, 1.9 => 2

ROUND_HALF_EVEN: rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5 => 2
- 1.6, 1.7, 1.8, 1.9 => 2
- 2.5 => 2

[SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SchemaUpdateOption)

`SchemaUpdateOption()`


Specifies an update to the destination table schema as a side effect of a load job.

[SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)

`SourceColumnMatch(value)`


Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat)

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

[SqlTypeNames](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SqlTypeNames)

`SqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.

[StandardSqlTypeNames](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames)

`StandardSqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.

[TimestampPrecision](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision)

`TimestampPrecision(value)`


Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

[UpdateMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode)

`UpdateMode(value)`


Specifies the kind of information to update in a dataset.

[WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition)

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryqueryscalarqueryparametertype__googlecloudbigqueryformat_op_51bc44.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryqueryscalarqueryparametertype__googlecloudbigqueryformat_opt_dae99e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryscalarqueryparametertype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType -->

# Class ScalarQueryParameterType (3.40.0)

`ScalarQueryParameterType(type_, *, name=None, description=None)`


Type representation for scalar query parameters.

## Parameters |
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
`google.cloud.bigquery.query.ScalarQueryParameterType` |
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
The new name of the query parameter type. If |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameterType` |
A new instance with updated name. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryformat_options_googlecloudbigquery_v2typesmodelclusteringmet_e9c2a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryformat_options.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options -->

# Module format_options (3.40.0)

API documentation for `bigquery.format_options`

module.

## Classes

[AvroOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions)

`AvroOptions()`


Options if source format is set to AVRO.

[ParquetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions)

`ParquetOptions()`


Additional options if the PARQUET source format is used.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelclusteringmetricsclusterfeaturevaluecategoricalvaluecategorycount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue.CategoryCount -->

# Class CategoryCount (3.40.0)

`CategoryCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the count of a single category within the cluster.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
`str`
The name of category. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
The count of training samples matching the category within the cluster. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerystandard_sql.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql -->

# Module standard_sql (3.40.0)

API documentation for `bigquery.standard_sql`

module.

## Classes

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType)

```
StandardSqlDataType(
type_kind: typing.Optional[
google.cloud.bigquery.enums.StandardSqlTypeNames
] = StandardSqlTypeNames.TYPE_KIND_UNSPECIFIED,
array_element_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
struct_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlStructType
] = None,
range_element_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
)
```


The type of a variable, e.g., a function argument.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType)

Examples:

```
INT64: {type_kind="INT64"}
ARRAY: {type_kind="ARRAY", array_element_type="STRING"}
STRUCT<x STRING, y ARRAY>: {
type_kind="STRUCT",
struct_type={
fields=[
{name="x", type={type_kind="STRING"}},
{
name="y",
type={type_kind="ARRAY", array_element_type="DATE"}
}
]
}
}
RANGE: {type_kind="RANGE", range_element_type="DATETIME"}
```


Parameters |
|
|---|---|
Name |
Description |
`type_kind` |
`typing.Optional[`
The top level type of this field. Can be any standard SQL data type, e.g. INT64, DATE, ARRAY. |
`array_element_type` |
`typing.Optional[StandardSqlDataType]`
The type of the array's elements, if type_kind is ARRAY. |
`struct_type` |
`typing.Optional[StandardSqlStructType]`
The fields of this struct, in order, if type_kind is STRUCT. |
`range_element_type` |
`typing.Optional[StandardSqlDataType]`
The type of the range's elements, if type_kind is RANGE. |

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField)

```
StandardSqlField(
name: typing.Optional[str] = None,
type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
)
```


A field or a column.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField)

Parameters |
|
|---|---|
Name |
Description |
`name` |
`typing.Optional[str]`
The name of this field. Can be absent for struct fields. |
`type` |
`typing.Optional[`
The type of this parameter. Absent if not explicitly specified. For example, CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType)

```
StandardSqlStructType(
fields: typing.Optional[
typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField]
] = None,
)
```


Type of a struct field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType)

Parameter |
|
|---|---|
Name |
Description |
`fields` |
`typing.Optional[typing.Iterable[`
The fields in this struct. |

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType)

```
StandardSqlTableType(
columns: typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField],
)
```
