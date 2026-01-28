---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/summary_class.html
fetched_at: 2026-01-28T07:37:51.776525
---

# Package Classes (3.40.0)

Summary of entries of Classes for bigquery.

## Classes

[Client](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client)

Client to bundle configuration needed for API requests.

[Project](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Project)

Wrapper for resource describing a BigQuery project.

[AccessEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.AccessEntry)

Represents grant of an access role to an entity.

An entry must have exactly one of the allowed
xref_EntityTypes. If anything but `view`

, `routine`

,
or `dataset`

are set, a `role`

is also required. `role`

is omitted for `view`

,
`routine`

, `dataset`

, because they are always read-only.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets).

[Condition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition)

Represents a textual expression in the Common Expression Language (CEL) syntax.

Typically used for filtering or policy rules, such as in IAM Conditions or BigQuery row/column access policies.

See:
[https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr](https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr)
[https://github.com/google/cel-spec](https://github.com/google/cel-spec)

[Dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset)

Datasets are containers for tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource-dataset)

[DatasetListItem](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetListItem)

A read-only dataset resource from a list operation.

For performance reasons, the BigQuery API only includes some of the dataset properties when listing datasets. Notably, xref_access_entries is missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for datasets.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets/list>
```

_.

[DatasetReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference)

DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

[Connection](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Connection)

DB-API Connection to Google BigQuery.

[Cursor](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor)

DB-API Cursor to Google BigQuery.

[DataError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DataError)

DB-API error due to problems with the processed data.

[DatabaseError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DatabaseError)

DB-API error related to the database.

[Error](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Error)

Exception representing all non-warning DB-API errors.

[IntegrityError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.IntegrityError)

DB-API error when integrity of the database is affected.

[InterfaceError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InterfaceError)

DB-API error related to the database interface.

[InternalError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InternalError)

DB-API error when the database encounters an internal error.

[NotSupportedError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.NotSupportedError)

DB-API error for operations not supported by the database or API.

[OperationalError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.OperationalError)

DB-API error related to the database operation.

These errors are not necessarily under the control of the programmer.

[ProgrammingError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.ProgrammingError)

DB-API exception raised for programming errors.

[Warning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Warning)

Exception raised for important DB-API warnings.

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration)

Custom encryption configuration (e.g., Cloud KMS keys).

[AutoRowIDs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.AutoRowIDs)

How to handle automatic insert IDs when inserting rows as a stream.

[BigLakeFileFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat)

API documentation for `bigquery.enums.BigLakeFileFormat`

class.

[BigLakeTableFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat)

API documentation for `bigquery.enums.BigLakeTableFormat`

class.

[Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression)

The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

[CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition)

Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

[DatasetView](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DatasetView)

DatasetView specifies which dataset information is returned.

[DecimalTargetType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType)

The data types that could be used as a target type when converting decimal values.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType)

.. versionadded:: 2.21.0

[DefaultPandasDTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes)

Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)

[DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat)

The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

[DeterminismLevel](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel)

Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

[Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Encoding)

The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

[EntityTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.EntityTypes)

Enum of allowed entity type names in AccessEntry

[JobCreationMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode)

Documented values for Job Creation Mode.

[KeyResultStatementKind](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.KeyResultStatementKind)

Determines which statement in the script represents the "key result".

The "key result" is used to populate the schema and query results of the script job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind)

[QueryApiMethod](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryApiMethod)

API method used to start the query. The default value is
`INSERT`

.

[QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryPriority)

Specifies a priority for the query. The default value is
`INTERACTIVE`

.

[RoundingMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.RoundingMode)

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

Specifies an update to the destination table schema as a side effect of a load job.

[SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)

Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat)

The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

[SqlTypeNames](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SqlTypeNames)

Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.

[StandardSqlTypeNames](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames)

Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.

[TimestampPrecision](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision)

Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

[UpdateMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode)

Specifies the kind of information to update in a dataset.

[WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition)

Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

[BigtableColumn](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn)

Options for a Bigtable column.

[BigtableColumnFamily](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily)

Options for a Bigtable column family.

[BigtableOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions)

Options that describe how to treat Bigtable tables as BigQuery tables.

[CSVOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions)

Options that describe how to treat CSV files as BigQuery tables.

[ExternalCatalogDatasetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogDatasetOptions)

Options defining open source compatible datasets living in the BigQuery catalog. Contains metadata of open source database, schema or namespace represented by the current dataset.

[ExternalCatalogTableOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalCatalogTableOptions)

Metadata about open source compatible table. The fields contained in these options correspond to hive metastore's table level properties.

[ExternalConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig)

Description of an external data source.

[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)

The format for external data files.

Note that the set of allowed values for external data sources is different
than the set used for loading data (see
[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)).

[GoogleSheetsOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions)

Options that describe how to treat Google Sheets as BigQuery tables.

[HivePartitioningOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions)

Options that configure hive partitioning.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions)

[AvroOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.AvroOptions)

Options if source format is set to AVRO.

[ParquetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions)

Additional options if the PARQUET source format is used.

[Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression)

The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

[CopyJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob)

Asynchronous job: copy data into a table from other tables.

[CopyJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig)

Configuration options for copy jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition)

Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

[DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat)

The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

[DmlStats](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats)

Detailed statistics for DML statements.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats](https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats)

[Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding)

The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

[ExtractJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob)

Asynchronous job: extract data from a table into Cloud Storage.

[ExtractJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig)

Configuration options for extract jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[IncrementalResultStats](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats)

IncrementalResultStats provides information about incremental query execution.

[LoadJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob)

Asynchronous job for loading data into a table.

Can load from Google Cloud Storage URIs or from a file.

[LoadJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig)

Configuration options for load jobs.

Set properties on the constructed configuration by using the property name
as the name of a keyword argument. Values which are unset or :data:`None`

use the BigQuery REST API default values. See the ```
BigQuery REST API
reference documentation
<https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad>
```

_
for a list of default values.

Required options differ based on the
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) value.
For example, the BigQuery API's default value for
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) is `"CSV"`

.
When loading a CSV file, either
[schema](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) must be set or
[autodetect](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) must be set to
:data:`True`

.

[OperationType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.OperationType)

Different operation types supported in table copy job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype)

[QueryJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob)

Asynchronous job: query tables.

[QueryJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig)

Configuration options for query jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[QueryPlanEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry)

QueryPlanEntry represents a single stage of a query execution plan.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage)
for the underlying API representation within query statistics.

[QueryPlanEntryStep](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep)

Map a single step in a query plan entry.

[QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority)

Specifies a priority for the query. The default value is
`INTERACTIVE`

.

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ReservationUsage)

Job resource usage for a reservation.

[SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)

Specifies an update to the destination table schema as a side effect of a load job.

[ScriptOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions)

Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions)

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame)

Stack frame showing the line/column/procedure name where the current evaluation happened.

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics)

Statistics for a child job of a script.

[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)

The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

[TimelineEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry)

TimelineEntry represents progress of a query job at a particular point in time.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample)
for the underlying API representation within query statistics.

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TransactionInfo)

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob)

A job whose type cannot be determined.

[WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition)

Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage)

Job resource usage for a reservation.

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame)

Stack frame showing the line/column/procedure name where the current evaluation happened.

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics)

Statistics for a child job of a script.

[SessionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo)

[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.TransactionInfo)

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob)

A job whose type cannot be determined.

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model)

Model represents a machine learning model resource.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models](https://cloud.google.com/bigquery/docs/reference/rest/v2/models)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference)

ModelReferences are pointers to models.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference)

[TransformColumn](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn)

TransformColumn represents a transform column feature.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

[ArrayQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter)

Named / positional query parameters for array values.

[ArrayQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType)

Type representation for array query parameters.

[ConnectionProperty](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty)

A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

[RangeQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter)

Named / positional query parameters for range values.

[RangeQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType)

Type representation for range query parameters.

[ScalarQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter)

Named / positional query parameters for scalar values.

[ScalarQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType)

Type representation for scalar query parameters.

[SqlParameterScalarTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes)

Supported scalar SQL query parameter types as type objects.

[StructQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter)

Name / positional query parameters for struct values.

[StructQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType)

Type representation for struct query parameters.

[UDFResource](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource)

Describe a single user-defined function (UDF) resource.

[DeterminismLevel](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel)

Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

[ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)

Options for the runtime of the external system.

[RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)

Configuration options for controlling remote BigQuery functions.

[Routine](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine)

Resource representing a user-defined routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines)

[RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)

Input/output argument of a function or a stored procedure.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument)

[RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference)

A pointer to a routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference)

[RoutineType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineType)

The fine-grained type of the routine.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype)

.. versionadded:: 2.22.0

[FieldElementType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.FieldElementType)

Represents the type of a field element.

[ForeignTypeInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.ForeignTypeInfo)

Metadata about the foreign data type definition such as the system in which the type is defined.

[PolicyTagList](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList)

Define Policy Tags for a column.

[SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)

Describe a single field within a table schema.

[SerDeInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo)

Serializer and deserializer information.

[StorageDescriptor](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.StorageDescriptor)

Contains information about how a table's data is stored and accessed by open source query engines.

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType)

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


[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField)

A field or a column.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField)

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType)

Type of a struct field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType)

A table type.

[BigLakeConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration)

Configuration for managed tables for Apache Iceberg, formerly known as BigLake.

[CloneDefinition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.CloneDefinition)

Information about base table and clone time of the clone.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition)

[ColumnReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ColumnReference)

The pair of the foreign key column and primary key column.

[ForeignKey](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey)

Represents a foreign key constraint on a table's columns.

[PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange)

Definition of the ranges for range partitioning.

[PrimaryKey](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PrimaryKey)

Represents the primary key constraint on a table's columns.

[RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)

Range-based partitioning configuration for a table.

[Row](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row)

A BigQuery row.

Values can be accessed by position (index), by key like a dict, or as properties.

[RowIterator](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator)

A class for iterating through HTTP/JSON API row list responses.

[SnapshotDefinition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.SnapshotDefinition)

Information about base table and snapshot time of the snapshot.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition)

[StreamingBuffer](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.StreamingBuffer)

Information about a table's streaming buffer.

See [https://cloud.google.com/bigquery/streaming-data-into-bigquery](https://cloud.google.com/bigquery/streaming-data-into-bigquery).

[Table](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table)

Tables represent a set of rows whose values correspond to a schema.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource-table](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource-table)

[TableConstraints](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints)

The TableConstraints defines the primary key and foreign key.

[TableListItem](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem)

A read-only table resource from a list operation.

For performance reasons, the BigQuery API only includes some of the table properties when listing tables. Notably, xref_schema and xref_num_rows are missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for tables.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list>
```

_.

[TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)

TableReferences are pointers to tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference)

[TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)

Configures time-based partitioning for a table.

[TimePartitioningType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType)

Specifies the type of time partitioning to perform.

[DeleteModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest)

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration)

[GetModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest)

[ListModelsRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest)

[ListModelsResponse](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse)

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model)

[AggregateClassificationMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.AggregateClassificationMetrics)

Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

[ArimaFittingMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics)

ARIMA model fitting metrics.

[ArimaForecastingMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics)

Model evaluation metrics for ARIMA forecasting models.

[ArimaSingleModelForecastingMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics.ArimaSingleModelForecastingMetrics)

Model evaluation metrics for a single ARIMA forecasting model.

[ArimaOrder](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaOrder)

Arima order, can be used for both non-seasonal and seasonal parts.

[BinaryClassificationMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics)

Evaluation metrics for binary classification/classifier models.

[BinaryConfusionMatrix](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics.BinaryConfusionMatrix)

Confusion matrix for binary classification models.

[ClusteringMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics)

Evaluation metrics for clustering models.

[Cluster](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster)

Message containing the information about one cluster.

[FeatureValue](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue)

Representative value of a single feature within the cluster.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[CategoricalValue](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue)

Representative value of a categorical feature.

[CategoryCount](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue.CategoryCount)

Represents the count of a single category within the cluster.

[DataFrequency](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataFrequency)

Type of supported data frequency for time series forecasting models.

[DataSplitMethod](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitMethod)

Indicates the method to split input data into multiple tables.

[DataSplitResult](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitResult)

Data split result. This contains references to the training and evaluation data tables that were used to train the model.

[DistanceType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DistanceType)

Distance metric used to compute the distance between two points.

[EvaluationMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.EvaluationMetrics)

Evaluation metrics of a model. These are either computed on all training data or just the eval data based on whether eval data was used during training. These are not present for imported models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[FeedbackType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.FeedbackType)

Indicates the training algorithm to use for matrix factorization models.

[GlobalExplanation](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation)

Global explanations containing the top most important features after training.

[Explanation](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation.Explanation)

Explanation for a single feature.

[HolidayRegion](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.HolidayRegion)

Type of supported holiday regions for time series forecasting models.

[KmeansEnums](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.KmeansEnums)

API documentation for `bigquery_v2.types.Model.KmeansEnums`

class.

[KmeansInitializationMethod](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.KmeansEnums.KmeansInitializationMethod)

Indicates the method used to initialize the centroids for KMeans clustering algorithm.

[LabelsEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LabelsEntry)

The abstract base class for a message.

[LearnRateStrategy](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LearnRateStrategy)

Indicates the learning rate optimization strategy to use.

[LossType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LossType)

Loss metric to evaluate model training performance.

[ModelType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ModelType)

Indicates the type of the Model.

[MultiClassClassificationMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics)

Evaluation metrics for multi-class classification/classifier models.

[ConfusionMatrix](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix)

Confusion matrix for multi-class classification models.

[Entry](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Entry)

A single entry in the confusion matrix.

[Row](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Row)

A single row in the confusion matrix.

[OptimizationStrategy](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.OptimizationStrategy)

Indicates the optimization strategy used for training.

[RankingMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RankingMetrics)

Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

[RegressionMetrics](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RegressionMetrics)

Evaluation metrics for regression and explicit feedback type matrix factorization models.

[SeasonalPeriod](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod)

API documentation for `bigquery_v2.types.Model.SeasonalPeriod`

class.

[SeasonalPeriodType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType)

API documentation for `bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType`

class.

[TrainingRun](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun)

Information about a single training query run for the model.

[IterationResult](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult)

Information about a single iteration of the training run.

[ArimaResult](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult)

(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

[ArimaCoefficients](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaCoefficients)

Arima coefficients.

[ArimaModelInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaModelInfo)

Arima model information.

[ClusterInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ClusterInfo)

Information about a single cluster for clustering model.

[TrainingOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions)

Options used in model training.

[LabelClassWeightsEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions.LabelClassWeightsEntry)

The abstract base class for a message.

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference)

Id path of a model.

[PatchModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest)

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType)

The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[TypeKind](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType.TypeKind)

API documentation for `bigquery_v2.types.StandardSqlDataType.TypeKind`

class.

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField)

A field or a column.

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType)

A table type

[TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.TableReference)

## Modules

[client](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client)

Client for interacting with the Google BigQuery API.

[dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset)

Define API Datasets.

[encryption_configuration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration)

Define class for the custom encryption configuration.

[enums](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums)

API documentation for `bigquery.enums`

module.

[external_config](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config)

Define classes that describe external data sources.

These are used for both Table.externalDataConfiguration and Job.configuration.query.tableDefinitions.

[format_options](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options)

API documentation for `bigquery.format_options`

module.

[base](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base)

Base classes and helpers for job classes.

[model](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model)

Define resources for the BigQuery ML Models API.

[query](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query)

BigQuery query processing.

[retry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.retry)

API documentation for `bigquery.retry`

module.

[schema](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema)

Schemas for BigQuery tables / queries.

[standard_sql](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql)

API documentation for `bigquery.standard_sql`

module.

[table](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table)

Define API Tables.