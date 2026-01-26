---
merged_at: 2026-01-26T21:00:49.255274
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

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelrankingmetrics__googlecloudbigquery_v2typesget_bfc35b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelrankingmetrics__googlecloudbigquery_v2typesgetm_c21693.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelrankingmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RankingMetrics -->

# Class RankingMetrics (3.40.0)

`RankingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

## Attributes |
|
|---|---|
Name |
Description |
`mean_average_precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users. |
`mean_squared_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not. |
`normalized_discounted_cumulative_gain` |
`google.protobuf.wrappers_pb2.DoubleValue`
A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings. |
`average_rank` |
`google.protobuf.wrappers_pb2.DoubleValue`
Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesgetmodelrequest_googlecloudbigquery_v2typesmodelarim_e5c321.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesgetmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest -->

# Class GetModelRequest (3.40.0)

`GetModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the requested model. |
`dataset_id` |
`str`
Required. Dataset ID of the requested model. |
`model_id` |
`str`
Required. Model ID of the requested model. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelarimaorder.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaOrder -->

# Class ArimaOrder (3.40.0)

`ArimaOrder(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima order, can be used for both non-seasonal and seasonal parts.

## Attributes |
|
|---|---|
Name |
Description |
`p` |
`int`
Order of the autoregressive part. |
`d` |
`int`
Order of the differencing part. |
`q` |
`int`
Order of the moving-average part. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrix_e2513d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrixr_cdfa84.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrixrow.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Row -->

# Class Row (3.40.0)

`Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single row in the confusion matrix.

## Attributes |
|
|---|---|
Name |
Description |
`actual_label` |
`str`
The original label of this row. |
`entries` |
`Sequence[`
Info describing predicted label distribution. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobwritedisposition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition -->

# Class WriteDisposition (3.40.0)

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configbigtableoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions -->

# Class BigtableOptions (3.40.0)

`BigtableOptions()`


Options that describe how to treat Bigtable tables as BigQuery tables.

## Properties

### column_families

List[`.external_config.BigtableColumnFamily`

]: List of
column families to expose in the table schema along with their types.

### ignore_unspecified_column_families

bool: If :data:`True`

, ignore columns not specified in
`column_families`

list. Defaults to :data:`False`

.

### read_rowkey_as_string

bool: If :data:`True`

, rowkey column families will be read and
converted to string. Defaults to :data:`False`

.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableOptions
```


Factory: construct a `.external_config.BigtableOptions`

instance given its API representation.

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
`BigtableOptions` |
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

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryenumsdefaultpandasdtypes_googlecloudbigquery_v2typesdelete_374680.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumsdefaultpandasdtypes_googlecloudbigquery_v2typesdeletem_eb9cfe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsdefaultpandasdtypes_googlecloudbigquery_v2typesdeletemo_525d76.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsdefaultpandasdtypes.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes -->

# Class DefaultPandasDTypes (3.40.0)

`DefaultPandasDTypes(value)`


Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesdeletemodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest -->

# Class DeleteModelRequest (3.40.0)

`DeleteModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the model to delete. |
`dataset_id` |
`str`
Required. Dataset ID of the model to delete. |
`model_id` |
`str`
Required. Model ID of the model to delete. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapiconnection.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Connection -->

# Class Connection (3.40.0)

`Connection(client=None, bqstorage_client=None, prefer_bqstorage_client=True)`


DB-API Connection to Google BigQuery.

## Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[google.cloud.bigquery.Client]`
A REST API client used to connect to BigQuery. If not passed, a client is created using default options inferred from the environment. |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A client that uses the faster BigQuery Storage API to fetch rows from BigQuery. If not passed, it is created using the same credentials as |
`prefer_bqstorage_client` |
`Optional[bool]`
Prefer the BigQuery Storage client over the REST client. If Storage client isn't available, fall back to the REST client. Defaults to |

## Methods

### close

`close()`


Close the connection and any cursors created from it.

Any BigQuery clients explicitly passed to the constructor are *not*
closed, only those created by the connection instance itself.

### commit

`commit()`


No-op, but for consistency raise an error if connection is closed.

### cursor

`cursor()`


Return a new cursor object.

Returns |
|
|---|---|
Type |
Description |
|
A DB-API cursor that uses this connection. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeltrainingrun_googlecloudbigqueryformat_optionspa_3af6f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingrun.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun -->

# Class TrainingRun (3.40.0)

`TrainingRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single training query run for the model.

## Attributes |
|
|---|---|
Name |
Description |
`training_options` |
Options that were used for this training run, includes user specified and default options that were used. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The start time of this training run. |
`results` |
`Sequence[`
Output of each iteration run, results.size() <= max_iterations.=""> |
`evaluation_metrics` |
The evaluation metrics over training/eval data that were computed at the end of training. |
`data_split_result` |
Data split result of the training run. Only set when the input data is actually split. |
`global_explanations` |
`Sequence[`
Global explanations for important features of the model. For multi-class models, there is one entry for each label class. For other models, there is only one entry in the list. |

## Classes

### IterationResult

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

### TrainingOptions

`TrainingOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options used in model training.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryformat_optionsparquetoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions -->

# Class ParquetOptions (3.40.0)

`ParquetOptions()`


Additional options if the PARQUET source format is used.

## Properties

### enable_list_inference

Indicates whether to use schema inference specifically for Parquet LIST logical type.

### enum_as_string

Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string)

### map_target_type

Indicates whether to simplify the representation of parquet maps to only show keys and values.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, bool],
) -> google.cloud.bigquery.format_options.ParquetOptions
```


Factory: construct an instance from a resource dict.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, bool]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
|
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, bool]` |
A dictionary in the format used by the BigQuery API. |
