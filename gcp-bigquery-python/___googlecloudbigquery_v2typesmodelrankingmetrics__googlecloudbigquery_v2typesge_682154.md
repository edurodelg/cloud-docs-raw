---
merged_at: 2026-01-25T15:38:56.569587
merged_files: 2
---

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
