---
merged_at: 2026-01-26T21:00:49.254818
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruntrainingoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryenumsdecimaltargettype_googlecloudbigquerytablesnapshotdef_0b8995.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumsdecimaltargettype_googlecloudbigquerytablesnapshotdefi_cb445d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsdecimaltargettype_googlecloudbigquerytablesnapshotdefin_1cbd57.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsdecimaltargettype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType -->

# Class DecimalTargetType (3.40.0)

`DecimalTargetType()`


The data types that could be used as a target type when converting decimal values.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType)

.. versionadded:: 2.21.0


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablesnapshotdefinition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.SnapshotDefinition -->

# Class SnapshotDefinition (3.40.0)

`SnapshotDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and snapshot time of the snapshot.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelseasonalperiod_googlecloudbigqueryjobsourceform_8fbecc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelseasonalperiod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod -->

# Class SeasonalPeriod (3.40.0)

`SeasonalPeriod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod`

class.

## Classes

### SeasonalPeriodType

`SeasonalPeriodType(value)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType`

class.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobsourceformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat -->

# Class SourceFormat (3.40.0)

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelkmeansenums_googlecloudbigqueryenumssourceform_40321e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelkmeansenums_googlecloudbigqueryenumssourceforma_a26ef4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelkmeansenums.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.KmeansEnums -->

# Class KmeansEnums (3.40.0)

`KmeansEnums(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.KmeansEnums`

class.

## Classes

### KmeansInitializationMethod

`KmeansInitializationMethod(value)`


Indicates the method used to initialize the centroids for KMeans clustering algorithm.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumssourceformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat -->

# Class SourceFormat (3.40.0)

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumswritedisposition_googlecloudbigqueryqueryudfresource.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumswritedisposition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition -->

# Class WriteDisposition (3.40.0)

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryudfresource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource -->

# Class UDFResource (3.40.0)

`UDFResource(udf_type, value)`


Describe a single user-defined function (UDF) resource.

## Parameters |
|
|---|---|
Name |
Description |
`udf_type` |
`str`
The type of the resource ('inlineCode' or 'resourceUri') |
`value` |
`str See: https://cloud.google.com/bigquery/user-defined-functions#api`
The inline code or resource URI. |

---
<!-- Source: N/A -->

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
