---
merged_at: 2026-01-25T15:38:56.572907
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_configcsvoptions_googlecloudbigqueryjobcopyjobconfi_b91225.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configcsvoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.CSVOptions -->

# Class CSVOptions (3.40.0)

`CSVOptions()`


Options that describe how to treat CSV files as BigQuery tables.

## Properties

### allow_jagged_rows

bool: If :data:`True`

, BigQuery treats missing trailing columns as
null values. Defaults to :data:`False`

.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.allow_jagged_rows](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.allow_jagged_rows)

### allow_quoted_newlines

bool: If :data:`True`

, quoted data sections that contain newline
characters in a CSV file are allowed. Defaults to :data:`False`

.

### encoding

str: The character encoding of the data.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.encoding)

### field_delimiter

str: The separator for fields in a CSV file. Defaults to comma (',').

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.field_delimiter](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.field_delimiter)

### null_markers

Optional[Iterable[str]]: A list of strings represented as SQL NULL values in a CSV file.

See[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.null_markers](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.null_markers)

### preserve_ascii_control_characters

bool: Indicates if the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '' to ' ') are preserved.

### quote_character

str: The value that is used to quote data sections in a CSV file.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.quote](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.quote)

### skip_leading_rows

int: The number of rows at the top of a CSV file.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.skip_leading_rows](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#CsvOptions.FIELDS.skip_leading_rows)

### source_column_match

Optional[[google.cloud.bigquery.enums.SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)]: Controls the
strategy used to match loaded columns to the schema. If not set, a sensible
default is chosen based on how the schema is provided. If autodetect is
used, then columns are matched by name. Otherwise, columns are matched by
position. This is done to keep the behavior backward-compatible.

Acceptable values are:

```
SOURCE_COLUMN_MATCH_UNSPECIFIED: Unspecified column name match option.
POSITION: matches by position. This assumes that the columns are ordered
the same way as the schema.
NAME: matches by name. This reads the header row as column names and
reorders columns to match the field names in the schema.
```


## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.external_config.CSVOptions`


Factory: construct a `.external_config.CSVOptions`

instance
given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
`CSVOptions` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, Any]` |
A dictionary in the format used by the BigQuery API. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobcopyjobconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig -->

# Class CopyJobConfig (3.40.0)

`CopyJobConfig(**kwargs)`


Configuration options for copy jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

## Properties

### create_disposition

[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition): Specifies behavior
for creating tables.

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### destination_expiration_time

google.cloud.bigquery.job.DestinationExpirationTime: The time when the destination table expires. Expired tables will be deleted and their storage reclaimed.

### job_timeout_ms

Optional parameter. Job timeout in milliseconds. If this time limit is exceeded, BigQuery might attempt to stop the job.
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.job_timeout_ms](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfiguration.FIELDS.job_timeout_ms)
e.g.

```
job_config = bigquery.QueryJobConfig( job_timeout_ms = 5000 )
or
job_config.job_timeout_ms = 5000
```


Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### labels

Dict[str, str]: Labels for the job.

This method always returns a dict. Once a job has been created on the server, its labels cannot be modified anymore.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### max_slots

The maximum rate of slot consumption to allow for this job.

If set, the number of slots used to execute the job will be throttled to try and keep its slot consumption below the requested rate. This feature is not generally available.

### operation_type

The operation to perform with this copy job.

### reservation

str: Optional. The reservation that job would use.

User can specify a reservation to execute the job. If reservation is not set, reservation is determined based on the rules defined by the reservation assignments. The expected format is projects/{project}/locations/{location}/reservations/{reservation}.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is not None or of string type. |

### write_disposition

[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition): Action that occurs if
the destination table already exists.

## Methods

### __setattr__

`__setattr__(name, value)`


Override to be able to raise error if an unknown property is being set

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.base._JobConfig`


Factory: construct a job configuration given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
A job configuration in the same representation as is returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job._JobConfig` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of the job config.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
A dictionary in the format used by the BigQuery API. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job -->

# Package job (3.40.0)

API documentation for `bigquery.job`

package.

## Classes

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
