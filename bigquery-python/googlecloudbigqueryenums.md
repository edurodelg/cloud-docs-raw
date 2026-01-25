---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums
fetched_at: 2026-01-25T03:12:43.920598
---

# Module enums (3.40.0)


      
      Save and categorize content based on your preferences.

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