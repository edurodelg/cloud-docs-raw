---
merged_at: 2026-01-26T21:00:49.254359
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerymodelmodelreference__googlecloudbigquerytableclonedefinitio_05595e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerymodelmodelreference__googlecloudbigquerytableclonedefinition_a3e562.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerymodelmodelreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference -->

# Class ModelReference (3.40.0)

`ModelReference()`


ModelReferences are pointers to models.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference)

## Properties

### dataset_id

str: ID of dataset containing the model.

### model_id

str: The model ID.

### path

URL path for the model's APIs.

### project

str: Project bound to the model

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.ModelReference
```


Factory: construct a model reference given its API representation.

### from_string

```
from_string(
model_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.model.ModelReference
```


Construct a model reference from model ID string.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `model_id` is not a fully-qualified table ID in standard SQL format. |

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this model reference.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytableclonedefinition_googlecloudbigqueryexternal_configexter_d60d74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytableclonedefinition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.CloneDefinition -->

# Class CloneDefinition (3.40.0)

`CloneDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and clone time of the clone.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configexternalsourceformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat -->

# Class ExternalSourceFormat (3.40.0)

`ExternalSourceFormat()`


The format for external data files.

Note that the set of allowed values for external data sources is different
than the set used for loading data (see
[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)).


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelclusteringmetricsclusterfeaturevalue_googleclou_d1e509.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelclusteringmetricsclusterfeaturevalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue -->

# Class FeatureValue (3.40.0)

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a single feature within the cluster.

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
`feature_column` |
`str`
The feature column name. |
`numerical_value` |
`google.protobuf.wrappers_pb2.DoubleValue`
The numerical feature value. This is the centroid value for this feature. This field is a member of `oneof` _ `value` .
|
`categorical_value` |
The categorical feature value. This field is a member of `oneof` _ `value` .
|

## Classes

### CategoricalValue

`CategoricalValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a categorical feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerymodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model -->

# Module model (3.40.0)

Define resources for the BigQuery ML Models API.

## Classes

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.Model)

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

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference)

`ModelReference()`


ModelReferences are pointers to models.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#modelreference)

[TransformColumn](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn)

`TransformColumn(resource: typing.Dict[str, typing.Any])`


TransformColumn represents a transform column feature.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerydatasetdatasetreference__googlecloudbigqueryexternal_configg_af4424.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydatasetdatasetreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference -->

# Class DatasetReference (3.40.0)

`DatasetReference(project: str, dataset_id: str)`


DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

## Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
The ID of the project |
`dataset_id` |
`str`
The ID of the dataset |

## Properties

### dataset_id

str: Dataset ID.

### path

str: URL path for the dataset based on project and dataset ID.

### project

str: Project ID of the dataset.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.DatasetReference`


Factory: construct a dataset reference given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
Dataset reference resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.DatasetReference` |
Dataset reference parsed from `resource` . |

### from_string

```
from_string(
dataset_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Construct a dataset reference from dataset ID string.

Parameters |
|
|---|---|
Name |
Description |
`dataset_id` |
`str`
A dataset ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `dataset_id` is not a fully-qualified dataset ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`DatasetReference .. rubric:: Examples >>> DatasetReference.from_string('my-project-id.some_dataset') DatasetReference('my-project-id', 'some_dataset')` |
Dataset reference parsed from `dataset_id` . |

### model

`model(model_id)`


Constructs a ModelReference.

Parameter |
|
|---|---|
Name |
Description |
`model_id` |
`str`
the ID of the model. |

Returns |
|
|---|---|
Type |
Description |
|
A ModelReference for a model in this dataset. |

### routine

`routine(routine_id)`


Constructs a RoutineReference.

Parameter |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
the ID of the routine. |

Returns |
|
|---|---|
Type |
Description |
|
A RoutineReference for a routine in this dataset. |

### table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

Parameter |
|
|---|---|
Name |
Description |
`table_id` |
`str`
The ID of the table. |

Returns |
|
|---|---|
Type |
Description |
|
A table reference for a table in this dataset. |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset reference

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
dataset reference represented as an API resource |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryexternal_configgooglesheetsoptions_googlecloudbigquery_v2typ_acb58e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryexternal_configgooglesheetsoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions -->

# Class GoogleSheetsOptions (3.40.0)

`GoogleSheetsOptions()`


Options that describe how to treat Google Sheets as BigQuery tables.

## Properties

### range

str: The range of a sheet that BigQuery will query from.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions.FIELDS.range](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions.FIELDS.range)

### skip_leading_rows

int: The number of rows at the top of a sheet that BigQuery will skip when reading the data.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.GoogleSheetsOptions
```


Factory: construct a `.external_config.GoogleSheetsOptions`

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
`GoogleSheetsOptions` |
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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult -->

# Class IterationResult (3.40.0)

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`google.protobuf.wrappers_pb2.Int32Value`
Index of the iteration, 0 based. |
`duration_ms` |
`google.protobuf.wrappers_pb2.Int64Value`
Time taken to run the iteration in milliseconds. |
`training_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the training data at the end of iteration. |
`eval_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the eval data at the end of iteration. |
`learn_rate` |
`float`
Learn rate used for this iteration. |
`cluster_infos` |
`Sequence[`
Information about top clusters for clustering models. |

## Classes

### ArimaResult

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

### ClusterInfo

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

---
<!-- Source: N/A -->

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
