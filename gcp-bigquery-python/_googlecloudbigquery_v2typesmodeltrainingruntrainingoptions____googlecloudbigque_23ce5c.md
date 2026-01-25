---
merged_at: 2026-01-25T15:38:56.569127
merged_files: 2
---

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
