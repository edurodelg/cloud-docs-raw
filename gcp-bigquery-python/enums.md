---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/enums
fetched_at: 2026-02-06T16:58:27.448458
---

# BigQuery Enums

*class* google.cloud.bigquery.enums.AutoRowIDs(value)

How to handle automatic insert IDs when inserting rows as a stream.

#### DISABLED(* = * )

#### GENERATE_UUID(* = * )

*class* google.cloud.bigquery.enums.BigLakeFileFormat()

#### FILE_FORMAT_UNSPECIFIED(* = 'FILE_FORMAT_UNSPECIFIED* )

The default unspecified value.

#### PARQUET(* = 'PARQUET* )

Apache Parquet format.

*class* google.cloud.bigquery.enums.BigLakeTableFormat()

#### ICEBERG(* = 'ICEBERG* )

Apache Iceberg format.

#### TABLE_FORMAT_UNSPECIFIED(* = 'TABLE_FORMAT_UNSPECIFIED* )

The default unspecified value.

*class* google.cloud.bigquery.enums.Compression(value)

The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

#### DEFLATE(* = 'DEFLATE* )

Specifies DEFLATE format.

#### GZIP(* = 'GZIP* )

Specifies GZIP format.

#### NONE(* = 'NONE* )

Specifies no compression.

#### SNAPPY(* = 'SNAPPY* )

Specifies SNAPPY format.

#### ZSTD(* = 'ZSTD* )

Specifies ZSTD format.

*class* google.cloud.bigquery.enums.CreateDisposition()

Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

#### CREATE_IF_NEEDED(* = 'CREATE_IF_NEEDED* )

If the table does not exist, BigQuery creates the table.

#### CREATE_NEVER(* = 'CREATE_NEVER* )

The table must already exist. If it does not, a ‘notFound’ error is returned in the job result.

*class* google.cloud.bigquery.enums.DatasetView(value)

DatasetView specifies which dataset information is returned.

#### ACL(* = 'ACL* )

View ACL information for the dataset, which defines dataset access for one or more entities.

#### DATASET_VIEW_UNSPECIFIED(* = 'DATASET_VIEW_UNSPECIFIED* )

The default value. Currently maps to the FULL view.

#### FULL(* = 'FULL* )

View both dataset metadata and ACL information.

#### METADATA(* = 'METADATA* )

View metadata information for the dataset, such as friendlyName, description, labels, etc.

*class* google.cloud.bigquery.enums.DecimalTargetType()

The data types that could be used as a target type when converting decimal values.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType)

**Versionadded:** New in version 2.21.0.

#### BIGNUMERIC(* = 'BIGNUMERIC* )

Decimal values could be converted to BIGNUMERIC type.

#### NUMERIC(* = 'NUMERIC* )

Decimal values could be converted to NUMERIC type.

#### STRING(* = 'STRING* )

Decimal values could be converted to STRING type.

*class* google.cloud.bigquery.enums.DefaultPandasDTypes(value)

Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)

#### BOOL_DTYPE(* = <object object* )

Specifies default bool dtype

#### DATE_DTYPE(* = <object object* )

Specifies default date dtype

#### INT_DTYPE(* = <object object* )

Specifies default integer dtype

#### RANGE_DATETIME_DTYPE(* = <object object* )

Specifies default range datetime dtype

#### RANGE_DATE_DTYPE(* = <object object* )

Specifies default range date dtype

#### RANGE_TIMESTAMP_DTYPE(* = <object object* )

Specifies default range timestamp dtype

#### TIME_DTYPE(* = <object object* )

Specifies default time dtype

*class* google.cloud.bigquery.enums.DestinationFormat()

The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

#### AVRO(* = 'AVRO* )

Specifies Avro format.

#### CSV(* = 'CSV* )

Specifies CSV format.

#### NEWLINE_DELIMITED_JSON(* = 'NEWLINE_DELIMITED_JSON* )

Specifies newline delimited JSON format.

#### PARQUET(* = 'PARQUET* )

Specifies Parquet format.

*class* google.cloud.bigquery.enums.DeterminismLevel()

Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

#### DETERMINISM_LEVEL_UNSPECIFIED(* = 'DETERMINISM_LEVEL_UNSPECIFIED* )

The determinism of the UDF is unspecified.

#### DETERMINISTIC(* = 'DETERMINISTIC* )

The UDF is deterministic, meaning that 2 function calls with the same inputs always produce the same result, even across 2 query runs.

#### NOT_DETERMINISTIC(* = 'NOT_DETERMINISTIC* )

The UDF is not deterministic.

*class* google.cloud.bigquery.enums.Encoding()

The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

#### ISO_8859_1(* = 'ISO-8859-1* )

Specifies ISO-8859-1 encoding.

#### UTF_8(* = 'UTF-8* )

Specifies UTF-8 encoding.

*class* google.cloud.bigquery.enums.EntityTypes(value)

Enum of allowed entity type names in AccessEntry

#### DATASET(* = 'dataset* )

#### DOMAIN(* = 'domain* )

#### GROUP_BY_EMAIL(* = 'groupByEmail* )

#### IAM_MEMBER(* = 'iamMember* )

#### ROUTINE(* = 'routine* )

#### SPECIAL_GROUP(* = 'specialGroup* )

#### USER_BY_EMAIL(* = 'userByEmail* )

#### VIEW(* = 'view* )

*class* google.cloud.bigquery.enums.JobCreationMode()

Documented values for Job Creation Mode.

#### JOB_CREATION_MODE_UNSPECIFIED(* = 'JOB_CREATION_MODE_UNSPECIFIED* )

Job creation mode is unspecified.

#### JOB_CREATION_OPTIONAL(* = 'JOB_CREATION_OPTIONAL* )

Job creation is optional.

Returning immediate results is prioritized. BigQuery will automatically determine if a Job needs to be created. The conditions under which BigQuery can decide to not create a Job are subject to change.

#### JOB_CREATION_REQUIRED(* = 'JOB_CREATION_REQUIRED* )

Job creation is always required.

*class* google.cloud.bigquery.enums.KeyResultStatementKind()

Determines which statement in the script represents the “key result”.

The “key result” is used to populate the schema and query results of the script job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind)

#### FIRST_SELECT(* = 'FIRST_SELECT* )

#### KEY_RESULT_STATEMENT_KIND_UNSPECIFIED(* = 'KEY_RESULT_STATEMENT_KIND_UNSPECIFIED* )

#### LAST(* = 'LAST* )

*class* google.cloud.bigquery.enums.QueryApiMethod(value)

API method used to start the query. The default value is
`INSERT`

.

#### INSERT(* = 'INSERT* )

Submit a query job by using the [jobs.insert REST API method](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert).

This supports all job configuration options.

#### QUERY(* = 'QUERY* )

Submit a query job by using the [jobs.query REST API method](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query).

Differences from `INSERT`

:

Many parameters and job configuration options, including job ID and destination table, cannot be used with this API method. See the

[jobs.query REST API documentation](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query)for the complete list of supported configuration options.API blocks up to a specified timeout, waiting for the query to finish.

The full job resource (including job statistics) may not be available. Call

or`reload()`

to get full job statistics and configuration.`get_job()`

`query()`

can raise API exceptions if the query fails, whereas the same errors don’t appear until callingwhen the`result()`

`INSERT`

API method is used.

*class* google.cloud.bigquery.enums.QueryPriority()

Specifies a priority for the query. The default value is
`INTERACTIVE`

.

#### BATCH(* = 'BATCH* )

Specifies batch priority.

#### INTERACTIVE(* = 'INTERACTIVE* )

Specifies interactive priority.

*class* google.cloud.bigquery.enums.RoundingMode(value)

Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

ROUNDING_MODE_UNSPECIFIED: will default to using ROUND_HALF_AWAY_FROM_ZERO.

ROUND_HALF_AWAY_FROM_ZERO: rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 * 1.1, 1.2, 1.3, 1.4 => 1 * 1.5, 1.6, 1.7, 1.8, 1.9 => 2

ROUND_HALF_EVEN: rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 * 1.1, 1.2, 1.3, 1.4 => 1 * 1.5 => 2 * 1.6, 1.7, 1.8, 1.9 => 2 * 2.5 => 2

#### ROUNDING_MODE_UNSPECIFIED(* = 'ROUNDING_MODE_UNSPECIFIED* )

#### ROUND_HALF_AWAY_FROM_ZERO(* = 'ROUND_HALF_AWAY_FROM_ZERO* )

#### ROUND_HALF_EVEN(* = 'ROUND_HALF_EVEN* )

*class* google.cloud.bigquery.enums.SchemaUpdateOption()

Specifies an update to the destination table schema as a side effect of a load job.

#### ALLOW_FIELD_ADDITION(* = 'ALLOW_FIELD_ADDITION* )

Allow adding a nullable field to the schema.

#### ALLOW_FIELD_RELAXATION(* = 'ALLOW_FIELD_RELAXATION* )

Allow relaxing a required field in the original schema to nullable.

*class* google.cloud.bigquery.enums.SourceColumnMatch(value)

Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

#### NAME(* = 'NAME* )

Matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.

#### POSITION(* = 'POSITION* )

Matches by position. This assumes that the columns are ordered the same way as the schema.

#### SOURCE_COLUMN_MATCH_UNSPECIFIED(* = 'SOURCE_COLUMN_MATCH_UNSPECIFIED* )

Unspecified column name match option.

*class* google.cloud.bigquery.enums.SourceFormat()

The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ ExternalSourceFormat](/python/docs/reference/bigquery/latest/reference#google.cloud.bigquery.external_config.ExternalSourceFormat)).

#### AVRO(* = 'AVRO* )

Specifies Avro format.

#### CSV(* = 'CSV* )

Specifies CSV format.

#### DATASTORE_BACKUP(* = 'DATASTORE_BACKUP* )

Specifies datastore backup format

#### NEWLINE_DELIMITED_JSON(* = 'NEWLINE_DELIMITED_JSON* )

Specifies newline delimited JSON format.

#### ORC(* = 'ORC* )

Specifies Orc format.

#### PARQUET(* = 'PARQUET* )

Specifies Parquet format.

*class* google.cloud.bigquery.enums.SqlTypeNames(value)

Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.

#### BIGDECIMAL(* = 'BIGNUMERIC* )

#### BIGNUMERIC(* = 'BIGNUMERIC* )

#### BOOL(* = 'BOOLEAN* )

#### BOOLEAN(* = 'BOOLEAN* )

#### BYTES(* = 'BYTES* )

#### DATE(* = 'DATE* )

#### DATETIME(* = 'DATETIME* )

#### DECIMAL(* = 'NUMERIC* )

#### FLOAT(* = 'FLOAT* )

#### FLOAT64(* = 'FLOAT* )

#### FOREIGN(* = 'FOREIGN* )

#### GEOGRAPHY(* = 'GEOGRAPHY* )

#### INT64(* = 'INTEGER* )

#### INTEGER(* = 'INTEGER* )

#### INTERVAL(* = 'INTERVAL* )

#### NUMERIC(* = 'NUMERIC* )

#### RANGE(* = 'RANGE* )

#### RECORD(* = 'RECORD* )

#### STRING(* = 'STRING* )

#### STRUCT(* = 'RECORD* )

#### TIME(* = 'TIME* )

#### TIMESTAMP(* = 'TIMESTAMP* )

*class* google.cloud.bigquery.enums.StandardSqlTypeNames(value)

Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.

#### ARRAY(* = 'ARRAY* )

#### BIGNUMERIC(* = 'BIGNUMERIC* )

#### BOOL(* = 'BOOL* )

#### BYTES(* = 'BYTES* )

#### DATE(* = 'DATE* )

#### DATETIME(* = 'DATETIME* )

#### FLOAT64(* = 'FLOAT64* )

#### FOREIGN(* = 'FOREIGN* )

#### GEOGRAPHY(* = 'GEOGRAPHY* )

#### INT64(* = 'INT64* )

#### INTERVAL(* = 'INTERVAL* )

#### JSON(* = 'JSON* )

#### NUMERIC(* = 'NUMERIC* )

#### RANGE(* = 'RANGE* )

#### STRING(* = 'STRING* )

#### STRUCT(* = 'STRUCT* )

#### TIME(* = 'TIME* )

#### TIMESTAMP(* = 'TIMESTAMP* )

#### TYPE_KIND_UNSPECIFIED(* = 'TYPE_KIND_UNSPECIFIED* )

*class* google.cloud.bigquery.enums.TimestampPrecision(value)

Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

#### MICROSECOND(* = Non* )

Default, for TIMESTAMP type with microsecond precision.

#### PICOSECOND(* = 1* )

For TIMESTAMP type with picosecond precision.

*class* google.cloud.bigquery.enums.UpdateMode(value)

Specifies the kind of information to update in a dataset.

#### UPDATE_ACL(* = 'UPDATE_ACL* )

Includes ACL information for the dataset, which defines dataset access for one or more entities.

#### UPDATE_FULL(* = 'UPDATE_FULL* )

Includes both dataset metadata and ACL information.

#### UPDATE_METADATA(* = 'UPDATE_METADATA* )

Includes metadata information for the dataset, such as friendlyName, description, labels, etc.

#### UPDATE_MODE_UNSPECIFIED(* = 'UPDATE_MODE_UNSPECIFIED* )

The default value. Behavior defaults to UPDATE_FULL.

*class* google.cloud.bigquery.enums.WriteDisposition()

Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

#### WRITE_APPEND(* = 'WRITE_APPEND* )

If the table already exists, BigQuery appends the data to the table.

#### WRITE_EMPTY(* = 'WRITE_EMPTY* )

If the table already exists and contains data, a ‘duplicate’ error is returned in the job result.

#### WRITE_TRUNCATE(* = 'WRITE_TRUNCATE* )

If the table already exists, BigQuery overwrites the table data.

#### WRITE_TRUNCATE_DATA(* = 'WRITE_TRUNCATE_DATA* )

For existing tables, truncate data but preserve existing schema and constraints.