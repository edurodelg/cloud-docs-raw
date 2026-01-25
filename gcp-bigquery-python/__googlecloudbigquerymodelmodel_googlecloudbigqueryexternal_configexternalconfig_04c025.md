---
merged_at: 2026-01-25T15:38:56.570477
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerymodelmodel_googlecloudbigqueryexternal_configexternalconfig.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerymodelmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model -->

# Class Model (3.40.0)

```
Model(
model_ref: typing.Optional[
typing.Union[google.cloud.bigquery.model.ModelReference, str]
],
)
```


Model represents a machine learning model resource.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models](https://cloud.google.com/bigquery/docs/reference/rest/v2/models)

## Properties

### best_trial_id

The best trial_id across all training runs.

Read-only.### created

Datetime at which the model was created (:data:`None`

until set from the server).

Read-only.

### dataset_id

ID of dataset containing the model.

### description

Description of the model (defaults to :data:`None`

).

### encryption_configuration

Custom encryption configuration for the model.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

See ```
protecting data with Cloud KMS keys
<
```

_
in the BigQuery documentation.[https://cloud.google.com/bigquery/docs/customer-managed-encryption>](https://cloud.google.com/bigquery/docs/customer-managed-encryption>);

### etag

ETag for the model resource (:data:`None`

until set from the server).

Read-only.

### expires

The datetime when this model expires.

If not present, the model will persist indefinitely. Expired models will be deleted and their storage reclaimed.

### feature_columns

Input feature columns that were used to train this model.

Read-only.

### friendly_name

Title of the table (defaults to :data:`None`

).

### label_columns

Label columns that were used to train this model.

The output of the model will have a `predicted_`

prefix to these columns.

Read-only.

### labels

Labels for the table.

This method always returns a dict. To change a model's labels, modify the dict,
then call `Client.update_model`

. To delete a label, set its value to
:data:`None`

before updating.

### location

The geographic location where the model resides.

This value is inherited from the dataset.

Read-only.

### model_id

The model ID.

### model_type

Type of the model resource.

Read-only.

### modified

Datetime at which the model was last modified (:data:`None`

until set from the server).

Read-only.

### path

URL path for the model's APIs.

### project

Project bound to the model.

### reference

A model reference pointing to this model.

Read-only.

### training_runs

Information for all training runs in increasing order of start time.

Dictionaries are in REST API format. See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#trainingrun](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#trainingrun)

Read-only.

### transform_columns

The input feature columns that were used to train this model. The output transform columns used to train this model.

See REST API:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

Read-only.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.Model
```


Factory: construct a model resource given its API representation

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configexternalconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig -->

# Class ExternalConfig (3.40.0)

`ExternalConfig(source_format)`


Description of an external data source.

## Parameter |
|
|---|---|
Name |
Description |
`source_format` |
`ExternalSourceFormat`
See |

## Properties

### autodetect

bool: If :data:`True`

, try to detect schema and format options
automatically.

### avro_options

Additional properties to set if `sourceFormat`

is set to AVRO.

### bigtable_options

Additional properties to set if `sourceFormat`

is set to BIGTABLE.

### compression

str: The compression type of the data source.

### connection_id

Optional[str]: ID of a BigQuery Connection API resource.

### csv_options

Additional properties to set if `sourceFormat`

is set to CSV.

### date_format

Optional[str]: Format used to parse DATE values. Supports C-style and SQL-style values.

### datetime_format

Optional[str]: Format used to parse DATETIME values. Supports C-style and SQL-style values.

### decimal_target_types

Possible SQL data types to which the source decimal values are converted.

.. versionadded:: 2.21.0

### google_sheets_options

Additional properties to set if `sourceFormat`

is set to
GOOGLE_SHEETS.

### hive_partitioning

Optional[`.external_config.HivePartitioningOptions`

]: When set, it configures hive partitioning support.

### ignore_unknown_values

bool: If :data:`True`

, extra values that are not represented in the
table schema are ignored. Defaults to :data:`False`

.

### max_bad_records

int: The maximum number of bad records that BigQuery can ignore when reading data.

### options

Source-specific options.

### parquet_options

Additional properties to set if `sourceFormat`

is set to PARQUET.

### reference_file_schema_uri

Optional[str]: When creating an external table, the user can provide a reference file with the table schema. This is enabled for the following formats:

AVRO, PARQUET, ORC

### schema

List[[SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)]: The schema
for the data.

### source_format

`.external_config.ExternalSourceFormat`

:
Format of external source.

### source_uris

List[str]: URIs that point to your data in Google Cloud.

### time_format

Optional[str]: Format used to parse TIME values. Supports C-style and SQL-style values.

### time_zone

Optional[str]: Time zone used when parsing timestamp values that do not have specific time zone information (e.g. 2024-04-20 12:34:56). The expected format is an IANA timezone string (e.g. America/Los_Angeles).

### timestamp_format

Optional[str]: Format used to parse TIMESTAMP values. Supports C-style and SQL-style values.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.ExternalConfig
```


Factory: construct an `.external_config.ExternalConfig`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of an |

Returns |
|
|---|---|
Type |
Description |
`ExternalConfig` |
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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobextractjobconfig_format_options.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobextractjobconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig -->

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

<!-- DOCUMENTO FUSIONADO: format_options.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/format_options -->

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
