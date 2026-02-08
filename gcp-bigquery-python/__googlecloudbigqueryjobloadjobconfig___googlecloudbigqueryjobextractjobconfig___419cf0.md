---
merged_at: 2026-02-08T01:20:52.894256
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig -->

# Class LoadJobConfig (3.40.0)

`LoadJobConfig(**kwargs)`


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

## Properties

### allow_jagged_rows

Optional[bool]: Allow missing trailing optional columns (CSV only).

### allow_quoted_newlines

Optional[bool]: Allow quoted data containing newline characters (CSV only).

### autodetect

Optional[bool]: Automatically infer the schema from a sample of the data.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.autodetect](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.autodetect)

### clustering_fields

Optional[List[str]]: Fields defining clustering for the table

(Defaults to :data:`None`

).

Clustering fields are immutable after table creation.

### column_name_character_map

Optional[google.cloud.bigquery.job.ColumnNameCharacterMap]: Character map supported for column names in CSV/Parquet loads. Defaults to STRICT and can be overridden by Project Config Service. Using this option with unsupported load formats will result in an error.

### connection_properties

Connection properties.

.. versionadded:: 3.7.0

### create_disposition

Optional[[google.cloud.bigquery.job.CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition)]: Specifies behavior
for creating tables.

### create_session

[Preview] If :data:`True`

, creates a new session, where
[session_info](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob) will contain a
random server generated session id.

If :data:`False`

, runs load job with an existing `session_id`

passed in
[connection_properties](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig),
otherwise runs load job in non-session mode.

.. versionadded:: 3.7.0

### date_format

Optional[str]: Date format used for parsing DATE values.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.date_format](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.date_format)

### datetime_format

Optional[str]: Date format used for parsing DATETIME values.

### decimal_target_types

Possible SQL data types to which the source decimal values are converted.

.. versionadded:: 2.21.0

### destination_encryption_configuration

Optional[[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration)]: Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### destination_table_description

Optional[str]: Description of the destination table.

### destination_table_friendly_name

Optional[str]: Name given to destination table.

### encoding

Optional[[google.cloud.bigquery.job.Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding)]: The character encoding of the
data.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.encoding)

### field_delimiter

Optional[str]: The separator for fields in a CSV file.

### hive_partitioning

Optional[`.external_config.HivePartitioningOptions`

]: [Beta] When set, it configures hive partitioning support.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.hive_partitioning_options](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.hive_partitioning_options)

### ignore_unknown_values

Optional[bool]: Ignore extra values not represented in the table schema.

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

### json_extension

Optional[str]: The extension to use for writing JSON data to BigQuery. Only supports GeoJSON currently.

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

### max_bad_records

Optional[int]: Number of invalid rows to ignore.

### max_slots

The maximum rate of slot consumption to allow for this job.

If set, the number of slots used to execute the job will be throttled to try and keep its slot consumption below the requested rate. This feature is not generally available.

### null_marker

Optional[str]: Represents a null value (CSV only).

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.null_marker](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.null_marker)

### null_markers

Optional[List[str]]: A list of strings represented as SQL NULL values in a CSV file.

See:[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.null_markers](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.null_markers)

### parquet_options

Optional[[google.cloud.bigquery.format_options.ParquetOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions)]: Additional
properties to set if `sourceFormat`

is set to PARQUET.

### preserve_ascii_control_characters

Optional[bool]: Preserves the embedded ASCII control characters when sourceFormat is set to CSV.

### projection_fields

Optional[List[str]]: If
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) is set to
"DATASTORE_BACKUP", indicates which entity properties to load into
BigQuery from a Cloud Datastore backup.

Property names are case sensitive and must be top-level properties. If no properties are specified, BigQuery loads all properties. If any named property isn't found in the Cloud Datastore backup, an invalid error is returned in the job result.

### quote_character

Optional[str]: Character used to quote data sections (CSV only).

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.quote](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.quote)

### range_partitioning

Optional[[google.cloud.bigquery.table.RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)]:
Configures range-based partitioning for destination table.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### reference_file_schema_uri

Optional[str]: When creating an external table, the user can provide a reference file with the table schema. This is enabled for the following formats:

AVRO, PARQUET, ORC

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

### schema

Optional[Sequence[Union[ [SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField), Mapping[str, Any] ]]]: Schema of the destination table.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.schema](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.schema)

### schema_update_options

Optional[List[[google.cloud.bigquery.job.SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)]]: Specifies
updates to the destination table schema to allow as a side effect of
the load job.

### skip_leading_rows

Optional[int]: Number of rows to skip when reading data (CSV only).

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


See:

### source_format

Optional[[google.cloud.bigquery.job.SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)]: File format of the data.

### time_format

Optional[str]: Date format used for parsing TIME values.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.time_format](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.time_format)

### time_partitioning

Optional[[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)]: Specifies time-based
partitioning for the destination table.

Only specify at most one of
[time_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) or
[range_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### time_zone

Optional[str]: Default time zone that will apply when parsing timestamp values that have no specific time zone.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.time_zone](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.time_zone)

### timestamp_format

Optional[str]: Date format used for parsing TIMESTAMP values.

### timestamp_target_precision

Optional[list[int]]: [Private Preview] Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.

Available for the formats: CSV.

For the CSV Format, Possible values include: None, [], or [6]: timestamp(6) for all auto detected TIMESTAMP columns. [6, 12]: timestamp(6) for all auto detected TIMESTAMP columns that have less than 6 digits of subseconds. timestamp(12) for all auto detected TIMESTAMP columns that have more than 6 digits of subseconds. [12]: timestamp(12) for all auto detected TIMESTAMP columns.

The order of the elements in this array is ignored. Inputs that have higher precision than the highest target precision in this array will be truncated.

### use_avro_logical_types

Optional[bool]: For loads of Avro data, governs whether Avro logical types are converted to their corresponding BigQuery types (e.g. TIMESTAMP) rather than raw types (e.g. INTEGER).

### write_disposition

Optional[[google.cloud.bigquery.job.WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition)]: Action that occurs if
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig -->

# Class ExtractJobConfig (3.40.0)

`ExtractJobConfig(**kwargs)`


Configuration options for extract jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

## Properties

### compression

[google.cloud.bigquery.job.Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression): Compression type to use for
exported files.

### destination_format

[google.cloud.bigquery.job.DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat): Exported file format.

### field_delimiter

str: Delimiter to use between fields in the exported data.

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

### print_header

bool: Print a header row in the exported data.

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

### use_avro_logical_types

bool: For loads of Avro data, governs whether Avro logical types are converted to their corresponding BigQuery types (e.g. TIMESTAMP) rather than raw types (e.g. INTEGER).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineType -->

# Class RoutineType (3.40.0)

`RoutineType()`


The fine-grained type of the routine.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinetype)

.. versionadded:: 2.22.0

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.retry -->

# Module retry (3.40.0)

API documentation for `bigquery.retry`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Warning -->

# Class Warning (3.40.0)

Exception raised for important DB-API warnings.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation -->

# Class GlobalExplanation (3.40.0)

`GlobalExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Global explanations containing the top most important features after training.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`Sequence[`
A list of the top global explanations. Sorted by absolute value of attribution in descending order. |
`class_label` |
`str`
Class label for this set of global explanations. Will be empty/null for binary logistic and linear regression models. Sorted alphabetically in descending order. |

## Classes

### Explanation

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation for a single feature.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.EvaluationMetrics -->

# Class EvaluationMetrics (3.40.0)

`EvaluationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics of a model. These are either computed on all training data or just the eval data based on whether eval data was used during training. These are not present for imported models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`regression_metrics` |
Populated for regression models and explicit feedback type matrix factorization models. This field is a member of `oneof` _ `metrics` .
|
`binary_classification_metrics` |
Populated for binary classification/classifier models. This field is a member of `oneof` _ `metrics` .
|
`multi_class_classification_metrics` |
Populated for multi-class classification/classifier models. This field is a member of `oneof` _ `metrics` .
|
`clustering_metrics` |
Populated for clustering models. This field is a member of `oneof` _ `metrics` .
|
`ranking_metrics` |
Populated for implicit feedback type matrix factorization models. This field is a member of `oneof` _ `metrics` .
|
`arima_forecasting_metrics` |
Populated for ARIMA models. This field is a member of `oneof` _ `metrics` .
|

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/format_options -->

# BigQuery Format Options

*class* google.cloud.bigquery.format_options.AvroOptions()

Options if source format is set to AVRO.

*classmethod* from_api_repr(resource: [Dict](https://docs.python.org/3/library/typing.html#typing.Dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [bool](https://docs.python.org/3/library/functions.html#bool)])

Factory: construct an instance from a resource dict.

**Parameters****resource**(*Dict**[**str**, *[*bool*](*]*) – Definition of a[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool))`AvroOptions`

instance in the same representation as is returned from the API.**Returns**Configuration parsed from

`resource`

.**Return type**`AvroOptions`


#### to_api_repr()

Build an API representation of this object.

*property* use_avro_logical_types(*: Optional[*[bool](https://docs.python.org/3/library/functions.html#bool) )

[bool](https://docs.python.org/3/library/functions.html#bool)

[Optional] If sourceFormat is set to ‘AVRO’, indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

*class* google.cloud.bigquery.format_options.ParquetOptions()

Additional options if the PARQUET source format is used.

*property* enable_list_inference(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

Indicates whether to use schema inference specifically for Parquet LIST logical type.

*property* enum_as_string(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string)

*classmethod* from_api_repr(resource: [Dict](https://docs.python.org/3/library/typing.html#typing.Dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [bool](https://docs.python.org/3/library/functions.html#bool)])

Factory: construct an instance from a resource dict.

**Parameters****resource**(*Dict**[**str**, *[*bool*](*]*) – Definition of a[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool))`ParquetOptions`

instance in the same representation as is returned from the API.**Returns**Configuration parsed from

`resource`

.**Return type**`ParquetOptions`


*property* map_target_type(*: Optional[Union[*[bool](https://docs.python.org/3/library/functions.html#bool), [str](https://docs.python.org/3/library/stdtypes.html#str)] )

[bool](https://docs.python.org/3/library/functions.html#bool),

[str](https://docs.python.org/3/library/stdtypes.html#str)]

Indicates whether to simplify the representation of parquet maps to only show keys and values.

#### to_api_repr()

Build an API representation of this object.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaModelInfo -->

# Class ArimaModelInfo (3.40.0)

`ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima model information.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
Non-seasonal order. |
`arima_coefficients` |
Arima coefficients. |
`arima_fitting_metrics` |
Arima fitting metrics. |
`has_drift` |
`bool`
Whether Arima model fitted with drift or not. It is always false when d is not 1. |
`time_series_id` |
`str`
The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used. |
`time_series_ids` |
`Sequence[str]`
The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |
`has_holiday_effect` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, holiday_effect is a part of time series decomposition result. |
`has_spikes_and_dips` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, spikes_and_dips is a part of time series decomposition result. |
`has_step_changes` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, step_changes is a part of time series decomposition result. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch -->

# Class SourceColumnMatch (3.40.0)

`SourceColumnMatch(value)`


Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Error -->

# Class Error (3.40.0)

Exception representing all non-warning DB-API errors.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DatabaseError -->

# Class DatabaseError (3.40.0)

DB-API error related to the database.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats -->

# Class DmlStats (3.40.0)

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Detailed statistics for DML statements.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats](https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats)

## Methods

### DmlStats

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Create new instance of DmlStats(inserted_row_count, deleted_row_count, updated_row_count)

### count

`count(value, /)`


Return number of occurrences of value.

### index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

Raises ValueError if the value is not present.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/enums -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics -->

# Class BinaryClassificationMetrics (3.40.0)

`BinaryClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for binary classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`binary_confusion_matrix_list` |
`Sequence[`
Binary confusion matrix at multiple thresholds. |
`positive_label` |
`str`
Label representing the positive class. |
`negative_label` |
`str`
Label representing the negative class. |

## Classes

### BinaryConfusionMatrix

`BinaryConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for binary classification models.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RegressionMetrics -->

# Class RegressionMetrics (3.40.0)

`RegressionMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for regression and explicit feedback type matrix factorization models.

## Attributes |
|
|---|---|
Name |
Description |
`mean_absolute_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean absolute error. |
`mean_squared_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean squared error. |
`mean_squared_log_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean squared log error. |
`median_absolute_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Median absolute error. |
`r_squared` |
`google.protobuf.wrappers_pb2.DoubleValue`
R^2 score. This corresponds to r2_score in ML.EVALUATE. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics.ArimaSingleModelForecastingMetrics -->

# Class ArimaSingleModelForecastingMetrics (3.40.0)

```
ArimaSingleModelForecastingMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Model evaluation metrics for a single ARIMA forecasting model.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
Non-seasonal order. |
`arima_fitting_metrics` |
Arima fitting metrics. |
`has_drift` |
`bool`
Is arima model fitted with drift or not. It is always false when d is not 1. |
`time_series_id` |
`str`
The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used. |
`time_series_ids` |
`Sequence[str]`
The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |
`has_holiday_effect` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, holiday_effect is a part of time series decomposition result. |
`has_spikes_and_dips` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, spikes_and_dips is a part of time series decomposition result. |
`has_step_changes` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, step_changes is a part of time series decomposition result. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model -->

# Class Model (3.40.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`etag` |
`str`
Output only. A hash of this resource. |
`model_reference` |
Required. Unique identifier for this model. |
`creation_time` |
`int`
Output only. The time when this model was created, in millisecs since the epoch. |
`last_modified_time` |
`int`
Output only. The time when this model was last modified, in millisecs since the epoch. |
`description` |
`str`
Optional. A user-friendly description of this model. |
`friendly_name` |
`str`
Optional. A descriptive name for this model. |
`labels` |
`Mapping[str, str]`
The labels associated with this model. You can use these to organize and group your models. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key. |
`expiration_time` |
`int`
Optional. The time when this model expires, in milliseconds since the epoch. If not present, the model will persist indefinitely. Expired models will be deleted and their storage reclaimed. The defaultTableExpirationMs property of the encapsulating dataset can be used to set a default expirationTime on newly created models. |
`location` |
`str`
Output only. The geographic location where the model resides. This value is inherited from the dataset. |
`encryption_configuration` |
Custom encryption configuration (e.g., Cloud KMS keys). This shows the encryption configuration of the model data while stored in BigQuery storage. This field can be used with PatchModel to update encryption key for an already encrypted model. |
`model_type` |
Output only. Type of the model resource. |
`training_runs` |
`Sequence[`
Output only. Information for all training runs in increasing order of start_time. |
`feature_columns` |
`Sequence[`
Output only. Input feature columns that were used to train this model. |
`label_columns` |
`Sequence[`
Output only. Label columns that were used to train this model. The output of the model will have a `predicted_`
prefix to these columns.
|
`best_trial_id` |
`int`
The best trial_id across all training runs. |

## Classes

### AggregateClassificationMetrics

```
AggregateClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

### ArimaFittingMetrics

`ArimaFittingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ARIMA model fitting metrics.

### ArimaForecastingMetrics

`ArimaForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model evaluation metrics for ARIMA forecasting models.

### ArimaOrder

`ArimaOrder(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima order, can be used for both non-seasonal and seasonal parts.

### BinaryClassificationMetrics

`BinaryClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for binary classification/classifier models.

### ClusteringMetrics

`ClusteringMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for clustering models.

### DataFrequency

`DataFrequency(value)`


Type of supported data frequency for time series forecasting models.

### DataSplitMethod

`DataSplitMethod(value)`


Indicates the method to split input data into multiple tables.

### DataSplitResult

`DataSplitResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data split result. This contains references to the training and evaluation data tables that were used to train the model.

### DistanceType

`DistanceType(value)`


Distance metric used to compute the distance between two points.

### EvaluationMetrics

`EvaluationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics of a model. These are either computed on all training data or just the eval data based on whether eval data was used during training. These are not present for imported models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### FeedbackType

`FeedbackType(value)`


Indicates the training algorithm to use for matrix factorization models.

### GlobalExplanation

`GlobalExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Global explanations containing the top most important features after training.

### HolidayRegion

`HolidayRegion(value)`


Type of supported holiday regions for time series forecasting models.

### KmeansEnums

`KmeansEnums(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.KmeansEnums`

class.

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### LearnRateStrategy

`LearnRateStrategy(value)`


Indicates the learning rate optimization strategy to use.

### LossType

`LossType(value)`


Loss metric to evaluate model training performance.

### ModelType

`ModelType(value)`


Indicates the type of the Model.

### MultiClassClassificationMetrics

```
MultiClassClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Evaluation metrics for multi-class classification/classifier models.

### OptimizationStrategy

`OptimizationStrategy(value)`


Indicates the optimization strategy used for training.

### RankingMetrics

`RankingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

### RegressionMetrics

`RegressionMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for regression and explicit feedback type matrix factorization models.

### SeasonalPeriod

`SeasonalPeriod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod`

class.

### TrainingRun

`TrainingRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single training query run for the model.
