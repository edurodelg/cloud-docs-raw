---
merged_at: 2026-01-29T15:47:08.983436
merged_files: 2
---


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
