---
merged_at: 2026-01-28T07:38:10.303324
merged_files: 2
---


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
