---
merged_at: 2026-02-02T16:19:10.390235
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep -->

# Class QueryPlanEntryStep (3.40.0)

`QueryPlanEntryStep(kind, substeps)`


Map a single step in a query plan entry.

## Parameters |
|
|---|---|
Name |
Description |
`kind` |
`str`
step type. |
`substeps` |
`List`
names of substeps. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntryStep`


Factory: construct instance from the JSON repr.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON representation of the entry. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.QueryPlanEntryStep` |
New instance built from the resource. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType -->

# Class StandardSqlTableType (3.40.0)

`StandardSqlTableType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A table type

## Attribute |
|
|---|---|
Name |
Description |
`columns` |
`Sequence[`
The columns in this table type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition -->

# Class CreateDisposition (3.40.0)

`CreateDisposition()`


Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics -->

# Class ClusteringMetrics (3.40.0)

`ClusteringMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for clustering models.

## Attributes |
|
|---|---|
Name |
Description |
`davies_bouldin_index` |
`google.protobuf.wrappers_pb2.DoubleValue`
Davies-Bouldin index. |
`mean_squared_distance` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean of squared distances between each sample to its cluster centroid. |
`clusters` |
`Sequence[`
Information for all clusters. |

## Classes

### Cluster

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.RoundingMode -->

# Class RoundingMode (3.40.0)

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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType -->

# Class StandardSqlDataType (3.40.0)

`StandardSqlDataType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

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
`type_kind` |
Required. The top level type of this field. Can be any standard SQL data type (e.g., "INT64", "DATE", "ARRAY"). |
`array_element_type` |
`google.cloud.bigquery_v2.types.StandardSqlDataType`
The type of the array's elements, if type_kind = "ARRAY". This field is a member of `oneof` _ `sub_type` .
|
`struct_type` |
The fields of this struct, in order, if type_kind = "STRUCT". This field is a member of `oneof` _ `sub_type` .
|

## Classes

### TypeKind

`TypeKind(value)`


API documentation for `bigquery_v2.types.StandardSqlDataType.TypeKind`

class.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TransactionInfo -->

# Class TransactionInfo (3.40.0)

`TransactionInfo(transaction_id: str)`


[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

## Methods

### TransactionInfo

`TransactionInfo(transaction_id: str)`


Create new instance of TransactionInfo(transaction_id,)

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition -->

# Class CreateDisposition (3.40.0)

`CreateDisposition()`


Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.OperationType -->

# Class OperationType (3.40.0)

`OperationType()`


Different operation types supported in table copy job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions -->

# Class TrainingOptions (3.40.0)

`TrainingOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options used in model training.

## Attributes |
|
|---|---|
Name |
Description |
`max_iterations` |
`int`
The maximum number of iterations in training. Used only for iterative training algorithms. |
`loss_type` |
Type of loss function used during training run. |
`learn_rate` |
`float`
Learning rate in training. Used only for iterative training algorithms. |
`l1_regularization` |
`google.protobuf.wrappers_pb2.DoubleValue`
L1 regularization coefficient. |
`l2_regularization` |
`google.protobuf.wrappers_pb2.DoubleValue`
L2 regularization coefficient. |
`min_relative_progress` |
`google.protobuf.wrappers_pb2.DoubleValue`
When early_stop is true, stops training when accuracy improvement is less than 'min_relative_progress'. Used only for iterative training algorithms. |
`warm_start` |
`google.protobuf.wrappers_pb2.BoolValue`
Whether to train a model from the last checkpoint. |
`early_stop` |
`google.protobuf.wrappers_pb2.BoolValue`
Whether to stop early when the loss doesn't improve significantly any more (compared to min_relative_progress). Used only for iterative training algorithms. |
`input_label_columns` |
`Sequence[str]`
Name of input label columns in training data. |
`data_split_method` |
The data split type for training and evaluation, e.g. RANDOM. |
`data_split_eval_fraction` |
`float`
The fraction of evaluation data over the whole input data. The rest of data will be used as training data. The format should be double. Accurate to two decimal places. Default value is 0.2. |
`data_split_column` |
`str`
The column to split data with. This column won't be used as a feature. 1. When data_split_method is CUSTOM, the corresponding column should be boolean. The rows with true value tag are eval data, and the false are training data. 2. When data_split_method is SEQ, the first DATA_SPLIT_EVAL_FRACTION rows (from smallest to largest) in the corresponding column are used as training data, and the rest are eval data. It respects the order in Orderable data types: https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data-type-properties |
`learn_rate_strategy` |
The strategy to determine learn rate for the current iteration. |
`initial_learn_rate` |
`float`
Specifies the initial learning rate for the line search learn rate strategy. |
`label_class_weights` |
`Mapping[str, float]`
Weights associated with each label class, for rebalancing the training data. Only applicable for classification models. |
`user_column` |
`str`
User column specified for matrix factorization models. |
`item_column` |
`str`
Item column specified for matrix factorization models. |
`distance_type` |
Distance type for clustering models. |
`num_clusters` |
`int`
Number of clusters for clustering models. |
`model_uri` |
`str`
Google Cloud Storage URI from which the model was imported. Only applicable for imported models. |
`optimization_strategy` |
Optimization strategy for training linear regression models. |
`hidden_units` |
`Sequence[int]`
Hidden units for dnn models. |
`batch_size` |
`int`
Batch size for dnn models. |
`dropout` |
`google.protobuf.wrappers_pb2.DoubleValue`
Dropout probability for dnn models. |
`max_tree_depth` |
`int`
Maximum depth of a tree for boosted tree models. |
`subsample` |
`float`
Subsample fraction of the training data to grow tree to prevent overfitting for boosted tree models. |
`min_split_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Minimum split loss for boosted tree models. |
`num_factors` |
`int`
Num factors specified for matrix factorization models. |
`feedback_type` |
Feedback type that specifies which algorithm to run for matrix factorization. |
`wals_alpha` |
`google.protobuf.wrappers_pb2.DoubleValue`
Hyperparameter for matrix factoration when implicit feedback type is specified. |
`kmeans_initialization_method` |
The method used to initialize the centroids for kmeans algorithm. |
`kmeans_initialization_column` |
`str`
The column used to provide the initial centroids for kmeans algorithm when kmeans_initialization_method is CUSTOM. |
`time_series_timestamp_column` |
`str`
Column to be designated as time series timestamp for ARIMA model. |
`time_series_data_column` |
`str`
Column to be designated as time series data for ARIMA model. |
`auto_arima` |
`bool`
Whether to enable auto ARIMA or not. |
`non_seasonal_order` |
A specification of the non-seasonal part of the ARIMA model: the three components (p, d, q) are the AR order, the degree of differencing, and the MA order. |
`data_frequency` |
The data frequency of a time series. |
`include_drift` |
`bool`
Include drift when fitting an ARIMA model. |
`holiday_region` |
The geographical region based on which the holidays are considered in time series modeling. If a valid value is specified, then holiday effects modeling is enabled. |
`time_series_id_column` |
`str`
The time series id column that was used during ARIMA model training. |
`time_series_id_columns` |
`Sequence[str]`
The time series id columns that were used during ARIMA model training. |
`horizon` |
`int`
The number of periods ahead that need to be forecasted. |
`preserve_input_structs` |
`bool`
Whether to preserve the input structs in output feature names. Suppose there is a struct A with field b. When false (default), the output feature name is A_b. When true, the output feature name is A.b. |
`auto_arima_max_order` |
`int`
The max value of non-seasonal p and q. |
`decompose_time_series` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, perform decompose time series and save the results. |
`clean_spikes_and_dips` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, clean spikes and dips in the input time series. |
`adjust_step_changes` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, detect step changes and make data adjustment in the input time series. |

## Classes

### LabelClassWeightsEntry

`LabelClassWeightsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob -->

# Class QueryJob (3.40.0)

`QueryJob(job_id, query, client, job_config=None)`


Asynchronous job: query tables.

## Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`str`
the job's ID, within the project belonging to |
`query` |
`str`
SQL query string. |
`client` |
A client which holds credentials and project configuration for the dataset (which requires a project). |
`job_config` |
`Optional[`
Extra configuration options for the query job. |

## Properties

### allow_large_results

See
[allow_large_results](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### billing_tier

Return billing tier from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.billing_tier](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.billing_tier)

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
Billing tier used by the job, or None if job is not yet complete. |

### cache_hit

Return whether or not query results were served from cache.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.cache_hit](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.cache_hit)

Returns |
|
|---|---|
Type |
Description |
`Optional[bool]` |
whether the query results were returned from cache, or None if job is not yet complete. |

### clustering_fields

See
[clustering_fields](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### configuration

The configuration for this query job.

### connection_properties

.. versionadded:: 2.29.0

### create_disposition

See
[create_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### create_session

See
[create_session](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

.. versionadded:: 2.29.0

### created

Datetime at which the job was created.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the creation time (None until set from the server). |

### ddl_operation_performed

Optional[str]: Return the DDL operation performed.

### ddl_target_routine

Optional[[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference)]: Return the DDL target routine, present
for CREATE/DROP FUNCTION/PROCEDURE queries.

### ddl_target_table

Optional[[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)]: Return the DDL target table, present
for CREATE/DROP TABLE/VIEW queries.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.ddl_target_table](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.ddl_target_table)

### default_dataset

See
[default_dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### destination

See
[destination](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### dry_run

See
[dry_run](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### ended

Datetime at which the job finished.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the end time (None until set from the server). |

### error_result

Output only. Final error result of the job.

If present, indicates that the job has completed and was unsuccessful.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result)

Returns |
|
|---|---|
Type |
Description |
`Optional[Mapping]` |
the error information (None until set from the server). |

### errors

Output only. The first errors encountered during the running of the job.

The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has not completed or was unsuccessful.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors)

Returns |
|
|---|---|
Type |
Description |
`Optional[List[Mapping]]` |
the error information (None until set from the server). |

### estimated_bytes_processed

Return the estimated number of bytes processed by the query.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
number of DML rows affected by the job, or None if job is not yet complete. |

### etag

ETag for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the ETag (None until set from the server). |

### flatten_results

See
[flatten_results](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### job_id

str: ID of the job.

### job_type

Type of job.

Returns |
|
|---|---|
Type |
Description |
`str` |
one of 'load', 'copy', 'extract', 'query'. |

### labels

Dict[str, str]: Labels for the job.

### location

str: Location where the job runs.

### maximum_billing_tier

See
[maximum_billing_tier](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### maximum_bytes_billed

See
[maximum_bytes_billed](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### num_child_jobs

The number of child jobs executed.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs)

### num_dml_affected_rows

Return the number of DML rows affected by the job.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
number of DML rows affected by the job, or None if job is not yet complete. |

### parent_job_id

Return the ID of the parent job.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.parent_job_id](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.parent_job_id)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
parent job id. |

### path

URL path for the job's APIs.

Returns |
|
|---|---|
Type |
Description |
`str` |
the path based on project and job ID. |

### priority

See
[priority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### project

Project bound to the job.

Returns |
|
|---|---|
Type |
Description |
`str` |
the project (derived from the client). |

### query

str: The query text used in this query job.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.query](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.query)

### query_id

[Preview] ID of a completed query.

This ID is auto-generated and not guaranteed to be populated.

### query_parameters

See
[query_parameters](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### query_plan

Return query plan from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.query_plan](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.query_plan)

Returns |
|
|---|---|
Type |
Description |
`List[` |
mappings describing the query plan, or an empty list if the query has not yet completed. |

### range_partitioning

See
[range_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### referenced_tables

Return referenced tables from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.referenced_tables](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.referenced_tables)

Returns |
|
|---|---|
Type |
Description |
`List[Dict]` |
mappings describing the query plan, or an empty list if the query has not yet completed. |

### reservation_id

str: Name of the primary reservation assigned to this job.

Note that this could be different than reservations reported in the reservation field if parent reservations were used to execute this job.

### reservation_usage

Job resource usage breakdown by reservation.

Returns |
|
|---|---|
Type |
Description |
`List[` |
Reservation usage stats. Can be empty if not set from the server. |

### schema

The schema of the results.

Present only for successful dry run of non-legacy SQL queries.

### schema_update_options

### script_statistics

Statistics for a child job of a script.

### search_stats

Returns a SearchStats object.

### self_link

URL for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the URL (None until set from the server). |

### session_info

[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

### slot_millis

Union[int, None]: Slot-milliseconds used by this query job.

### started

Datetime at which the job was started.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the start time (None until set from the server). |

### state

Output only. Running state of the job.

Valid states include 'PENDING', 'RUNNING', and 'DONE'.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.state](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.state)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the state (None until set from the server). |

### statement_type

Return statement type from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.statement_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.statement_type)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
type of statement used by the job, or None if job is not yet complete. |

### table_definitions

See
[table_definitions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### time_partitioning

See
[time_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### timeline

List(TimelineEntry): Return the query execution timeline from job statistics.

### total_bytes_billed

Return total bytes billed from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
Total bytes processed by the job, or None if job is not yet complete. |

### total_bytes_processed

Return total bytes processed from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
Total bytes processed by the job, or None if job is not yet complete. |

### transaction_info

Information of the multi-statement transaction if this job is part of one.

Since a scripting query job can execute multiple transactions, this
property is only expected on child jobs. Use the
[list_jobs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client) method with the
`parent_job`

parameter to iterate over child jobs.

.. versionadded:: 2.24.0

### udf_resources

See
[udf_resources](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### undeclared_query_parameters

Return undeclared query parameters from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`List[Union[ ` |
Undeclared parameters, or an empty list if the query has not yet completed. |

### use_legacy_sql

See
[use_legacy_sql](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### use_query_cache

See
[use_query_cache](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### user_email

E-mail address of user who submitted the job.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the URL (None until set from the server). |

### write_disposition

See
[write_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

## Methods

### add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

If the operation is not already complete, this will start a helper thread to poll for the status of the operation in the background.

Parameter |
|
|---|---|
Name |
Description |
`fn` |
`Callable[Future]`
The callback to execute when the operation is complete. |

### cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel)

Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Boolean indicating that the cancel request was sent. |

### cancelled

`cancelled()`


Check if the job has been cancelled.

This always returns False. It's not possible to check if a job was
cancelled in the API. This method is here to satisfy the interface
for `google.api_core.future.Future`

.

Returns |
|
|---|---|
Type |
Description |
`bool` |
False |

### done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`reload` |
`Optional[bool]`
If |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. If the job state is |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if the job is complete, False otherwise. |

### exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

See the documentation for the `result`

method for details on how
this method operates, as both `result`

and this method rely on the
exact same polling logic. The only difference is that this method does
not accept `retry`

and `polling`

arguments but relies on the default ones
instead.

Parameter |
|
|---|---|
Name |
Description |
`timeout` |
`int`
How long to wait for the operation to complete. |

Returns |
|
|---|---|
Type |
Description |
`Optional[google.api_core.GoogleAPICallError]` |
The operation's error. |

### exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Boolean indicating existence of the job. |

### from_api_repr

`from_api_repr(resource: dict, client: Client) -> QueryJob`


Factory: construct a job given its API representation

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
dataset job representation returned from the API |
`client` |
Client which holds credentials and project configuration for the dataset. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.QueryJob` |
Job parsed from `resource` . |

### reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |

### result

```
result(
page_size: typing.Optional[int] = None,
max_results: typing.Optional[int] = None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[typing.Union[float, object]] = object,
start_index: typing.Optional[int] = None,
job_retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
) -> typing.Union[RowIterator, google.cloud.bigquery.table._EmptyRowIterator]
```


Start the job and wait for it to complete and get the result.

Parameters |
|
|---|---|
Name |
Description |
`page_size` |
`Optional[int]`
The maximum number of rows in each page of results from this request. Non-positive values are ignored. |
`max_results` |
`Optional[int]`
The maximum total number of rows from this request. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the call that retrieves rows. This only applies to making RPC calls. It isn't used to retry failed jobs. This has a reasonable default that should only be overridden with care. If the job state is |
`timeout` |
`Optional[Union[float, google.api_core.future.polling.PollingFuture._DEFAULT_VALUE, ]]`
The number of seconds to wait for the underlying HTTP transport before using |
`start_index` |
`Optional[int]`
The zero-based index of the starting row to read. |
`job_retry` |
`Optional[google.api_core.retry.Retry]`
How to retry failed jobs. The default retries rate-limit-exceeded errors. Passing |

Exceptions |
|
|---|---|
Type |
Description |
`google.api_core.exceptions.GoogleAPICallError` |
If the job failed and retries aren't successful. |
`concurrent.futures.TimeoutError` |
If the job did not complete in the given timeout. |
`TypeError` |
If Non-`None` and non-default `job_retry` is provided and the job is not retryable. |

Returns |
|
|---|---|
Type |
Description |
|
Iterator of row data
`total_rows` attribute set, which counts the total number of rows **in the result set** (this is distinct from the total number of rows in the current page: `iterator.page.num_items` ). If the query is a special query that produces no results, e.g. a DDL query, an `_EmptyRowIterator` instance is returned. |

### running

`running()`


True if the operation is currently running.

### set_exception

`set_exception(exception)`


Set the Future's exception.

### set_result

`set_result(result)`


Set the Future's result.

### to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.

### to_arrow

```
to_arrow(
progress_bar_type: typing.Optional[str] = None,
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
) -> pyarrow.Table
```


[Beta] Create a class:`pyarrow.Table`

by loading all pages of a
table or query.

Parameters |
|
|---|---|
Name |
Description |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This API is a billable API. This method requires |
`create_bqstorage_client` |
`Optional[bool]`
If |
`max_results` |
`Optional[int]`
Maximum number of rows to include in the result. No limit by default. .. versionadded:: 2.21.0 |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `pyarrow` library cannot be imported. .. versionadded:: 1.17.0 |

### to_dataframe

```
to_dataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
geography_as_object: bool = False,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
date_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.DATE_DTYPE,
datetime_dtype: typing.Optional[typing.Any] = None,
time_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.TIME_DTYPE,
timestamp_dtype: typing.Optional[typing.Any] = None,
range_date_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATE_DTYPE,
range_datetime_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATETIME_DTYPE,
range_timestamp_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_TIMESTAMP_DTYPE,
) -> pandas.DataFrame
```


Return a pandas DataFrame from a QueryJob

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This API is a billable API. This method requires the |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`create_bqstorage_client` |
`Optional[bool]`
If |
`max_results` |
`Optional[int]`
Maximum number of rows to include in the result. No limit by default. .. versionadded:: 2.21.0 |
`geography_as_object` |
`Optional[bool]`
If |
`bool_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`int_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`float_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`string_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`date_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`datetime_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`time_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`timestamp_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`range_date_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype, such as: .. code-block:: python pandas.ArrowDtype(pyarrow.struct( [("start", pyarrow.date32()), ("end", pyarrow.date32())] )) to convert BigQuery RANGE
|
`range_datetime_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype, such as: .. code-block:: python pandas.ArrowDtype(pyarrow.struct( [ ("start", pyarrow.timestamp("us")), ("end", pyarrow.timestamp("us")), ] )) to convert BigQuery RANGE
|
`range_timestamp_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype, such as: .. code-block:: python pandas.ArrowDtype(pyarrow.struct( [ ("start", pyarrow.timestamp("us", tz="UTC")), ("end", pyarrow.timestamp("us", tz="UTC")), ] )) to convert BigQuery RANGE
|

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `pandas` library cannot be imported, or the bigquery_storage_v1 module is required but cannot be imported. Also if `geography_as_object` is `True` , but the `shapely` library cannot be imported. |

Returns |
|
|---|---|
Type |
Description |
`pandas.DataFrame` |
A `pandas.DataFrame` populated with row data and column headers from the query results. The column headers are derived from the destination table's schema. |

### to_geodataframe

```
to_geodataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
geography_column: typing.Optional[str] = None,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
) -> geopandas.GeoDataFrame
```


Return a GeoPandas GeoDataFrame from a QueryJob

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This API is a billable API. This method requires the |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`create_bqstorage_client` |
`Optional[bool]`
If |
`max_results` |
`Optional[int]`
Maximum number of rows to include in the result. No limit by default. .. versionadded:: 2.21.0 |
`geography_column` |
`Optional[str]`
If there are more than one GEOGRAPHY column, identifies which one to use to construct a GeoPandas GeoDataFrame. This option can be ommitted if there's only one GEOGRAPHY column. |
`bool_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`int_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`float_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`string_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `geopandas` library cannot be imported, or the bigquery_storage_v1 module is required but cannot be imported. .. versionadded:: 2.24.0 |

Returns |
|
|---|---|
Type |
Description |
`geopandas.GeoDataFrame` |
A `geopandas.GeoDataFrame` populated with row data and column headers from the query results. The column headers are derived from the destination table's schema. |
