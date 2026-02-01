---
merged_at: 2026-02-01T08:10:00.335217
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor -->

# Class Cursor (3.40.0)

`Cursor(connection)`


DB-API Cursor to Google BigQuery.

## Parameter |
|
|---|---|
Name |
Description |
`connection` |
A DB-API connection to Google BigQuery. |

## Properties

### query_job

[google.cloud.bigquery.job](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job).query.QueryJob | None: The query job
created by the last `execute`

call, if a query job was created.*()*

## Methods

### close

`close()`


Mark the cursor as closed, preventing its further use.

### execute

`execute(operation, parameters=None, job_id=None, job_config=None)`


Prepare and execute a database operation.

A`datetime.datetime`

parameter without timezone information uses
the 'DATETIME' BigQuery type (example: Global Pi Day Celebration
March 14, 2017 at 1:59pm). A `datetime.datetime`

parameter with
timezone information uses the 'TIMESTAMP' BigQuery type (example:
a wedding on April 29, 2011 at 11am, British Summer Time).
```
For more information about BigQuery data types, see:
https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types
`STRUCT`/`RECORD` and `REPEATED` query parameters are not
yet supported. See:
https://github.com/GoogleCloudPlatform/google-cloud-python/issues/3524
```


Parameters |
|
|---|---|
Name |
Description |
`operation` |
`str`
A Google BigQuery query string. |
`parameters` |
`Union[Mapping[str, Any], Sequence[Any]]`
(Optional) dictionary or sequence of parameter values. |
`job_id` |
`str None`
(Optional and discouraged) The job ID to use when creating the query job. For best performance and reliability, manually setting a job ID is discouraged. |
`job_config` |
(Optional) Extra configuration options for the query job. |

### executemany

`executemany(operation, seq_of_parameters)`


Prepare and execute a database operation multiple times.

Parameters |
|
|---|---|
Name |
Description |
`operation` |
`str`
A Google BigQuery query string. |
`seq_of_parameters` |
`Union[Sequence[Mapping[str, Any], Sequence[Any]]]`
Sequence of many sets of parameter values. |

### fetchall

`fetchall()`


Fetch all remaining results from the last `execute*()`

call.

Exceptions |
|
|---|---|
Type |
Description |
|
if called before `execute()` . |

Returns |
|
|---|---|
Type |
Description |
`List[Tuple]` |
A list of all the rows in the results. |

### fetchmany

`fetchmany(size=None)`


Fetch multiple results from the last `execute*()`

call.

Parameter |
|
|---|---|
Name |
Description |
`size` |
`int`
(Optional) Maximum number of rows to return. Defaults to the |

Exceptions |
|
|---|---|
Type |
Description |
|
if called before `execute()` . |

Returns |
|
|---|---|
Type |
Description |
`List[Tuple]` |
A list of rows. |

### fetchone

`fetchone()`


Fetch a single row from the results of the last `execute*()`

call.

Exceptions |
|
|---|---|
Type |
Description |
|
if called before `execute()` . |

Returns |
|
|---|---|
Type |
Description |
`Tuple` |
A tuple representing a row or `None` if no more data is available. |

### setinputsizes

`setinputsizes(sizes)`


No-op, but for consistency raise an error if cursor is closed.

### setoutputsize

`setoutputsize(size, column=None)`


No-op, but for consistency raise an error if cursor is closed.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter -->

# Class ArrayQueryParameter (3.40.0)

`ArrayQueryParameter(name, array_type, values)`


Named / positional query parameters for array values.

## Parameters |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ArrayQueryParameter`


Factory: construct parameter from JSON resource.

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
`google.cloud.bigquery.query.ArrayQueryParameter` |
Instance |

### positional

```
positional(
array_type: str, values: list
) -> google.cloud.bigquery.query.ArrayQueryParameter
```


Factory for positional parameters.

Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ArrayQueryParameter` |
Instance without name |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue -->

# Class CategoricalValue (3.40.0)

`CategoricalValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a categorical feature.

## Attribute |
|
|---|---|
Name |
Description |
`category_counts` |
`Sequence[`
Counts of all categories for the categorical feature. If there are more than ten categories, we return top ten (by count) and return one more CategoryCount with category "*OTHER*" and count as aggregate counts of remaining categories. |

## Classes

### CategoryCount

`CategoryCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the count of a single category within the cluster.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix -->

# Class ConfusionMatrix (3.40.0)

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Confidence threshold used when computing the entries of the confusion matrix. |
`rows` |
`Sequence[`
One row per actual label. |

## Classes

### Entry

`Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single entry in the confusion matrix.

### Row

`Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single row in the confusion matrix.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalConfig -->

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
