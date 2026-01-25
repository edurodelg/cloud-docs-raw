---
merged_at: 2026-01-25T15:38:56.573344
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigquery_v2typespatchmodelrequest_googlecloudbigquery_v2typesmodel_bc247f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typespatchmodelrequest_googlecloudbigquery_v2typesmodelt_c01c43.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typespatchmodelrequest_googlecloudbigquery_v2typesmodeltr_c879f6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typespatchmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest -->

# Class PatchModelRequest (3.40.0)

`PatchModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the model to patch. |
`dataset_id` |
`str`
Required. Dataset ID of the model to patch. |
`model_id` |
`str`
Required. Model ID of the model to patch. |
`model` |
Required. Patched model. Follows RFC5789 patch semantics. Missing fields are not updated. To clear a field, explicitly set to default value. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresultarimaresultarimacoefficients.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaCoefficients -->

# Class ArimaCoefficients (3.40.0)

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

## Attributes |
|
|---|---|
Name |
Description |
`auto_regressive_coefficients` |
`Sequence[float]`
Auto-regressive coefficients, an array of double. |
`moving_average_coefficients` |
`Sequence[float]`
Moving-average coefficients, an array of double. |
`intercept_coefficient` |
`float`
Intercept coefficient, just a double not an array. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelevaluationmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.EvaluationMetrics -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeltrainingruniterationresultarimaresultarimamodel_3c90fc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresultarimaresultarimamodelinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaModelInfo -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeltrainingruntrainingoptionslabelclassweightsentr_993cab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruntrainingoptionslabelclassweightsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.TrainingOptions.LabelClassWeightsEntry -->

# Class LabelClassWeightsEntry (3.40.0)

`LabelClassWeightsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytableforeignkey.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey -->

# Class ForeignKey (3.40.0)

```
ForeignKey(
name: str,
referenced_table: google.cloud.bigquery.table.TableReference,
column_references: typing.List[google.cloud.bigquery.table.ColumnReference],
)
```


Represents a foreign key constraint on a table's columns.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.ForeignKey
```


Create an instance from API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigquery_v2typesmodeltrainingruniterationresultclusterinfo_googlec_a0e4d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodeltrainingruniterationresultclusterinfo_googlecl_4d7f3a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeltrainingruniterationresultclusterinfo_googleclo_d62953.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresultclusterinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ClusterInfo -->

# Class ClusterInfo (3.40.0)

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`cluster_radius` |
`google.protobuf.wrappers_pb2.DoubleValue`
Cluster radius, the average distance from centroid to each point assigned to the cluster. |
`cluster_size` |
`google.protobuf.wrappers_pb2.Int64Value`
Cluster size, the total number of points assigned to the cluster. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobscriptstatistics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics -->

# Class ScriptStatistics (3.40.0)

`ScriptStatistics(resource)`


Statistics for a child job of a script.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### evaluation_kind

str: Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

### stack_frames

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryschemaserdeinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo -->

# Class SerDeInfo (3.40.0)

```
SerDeInfo(
serialization_library: str,
name: typing.Optional[str] = None,
parameters: typing.Optional[dict[str, str]] = None,
)
```


Serializer and deserializer information.

## Parameters |
|
|---|---|
Name |
Description |
`serialization_library` |
`str`
Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters. |
`name` |
`Optional[str]`
Name of the SerDe. The maximum length is 256 characters. |

## Properties

### name

Optional. Name of the SerDe. The maximum length is 256 characters.

### parameters

Optional. Key-value pairs that define the initialization parameters for the serialization library. Maximum size 10 Kib.

### serialization_library

Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.SerDeInfo`


Factory: constructs an instance of the class (cls) given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, Any]`
API representation of the object to be instantiated. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytabletablelistitem.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem -->

# Class TableListItem (3.40.0)

`TableListItem(resource)`


A read-only table resource from a list operation.

For performance reasons, the BigQuery API only includes some of the table properties when listing tables. Notably, xref_schema and xref_num_rows are missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for tables.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list>
```

_.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
A table-like resource object from a table list response. A |

## Properties

### clustering_fields

Union[List[str], None]: Fields defining clustering for the table

(Defaults to :data:`None`

).

Clustering fields are immutable after table creation.

### created

Union[datetime.datetime, None]: Datetime at which the table was
created (:data:`None`

until set from the server).

### expires

Union[datetime.datetime, None]: Datetime at which the table will be deleted.

### friendly_name

Union[str, None]: Title of the table (defaults to :data:`None`

).

### full_table_id

Union[str, None]: ID for the table (:data:`None`

until set from the
server).

In the format `project_id:dataset_id.table_id`

.

### labels

Dict[str, str]: Labels for the table.

This method always returns a dict. To change a table's labels,
modify the dict, then call `Client.update_table`

. To delete a
label, set its value to :data:`None`

before updating.

### partition_expiration

Union[int, None]: Expiration time in milliseconds for a partition.

If this property is set and `type_`

is not set, `type_`

will default to `TimePartitioningType.DAY`

.

### partitioning_type

Union[str, None]: Time partitioning of the table if it is
partitioned (Defaults to :data:`None`

).

### reference

A xref_TableReference pointing to this table.

Returns |
|
|---|---|
Type |
Description |
|
pointer to this table. |

### table_type

Union[str, None]: The type of the table (:data:`None`

until set from
the server).

Possible values are `'TABLE'`

, `'VIEW'`

, or `'EXTERNAL'`

.

### time_partitioning

[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning): Configures time-based
partitioning for a table.

### view_use_legacy_sql

bool: Specifies whether to execute the view with Legacy or Standard SQL.

This boolean specifies whether to execute the view with Legacy SQL
(:data:`True`

) or Standard SQL (:data:`False`

). The client side default is
:data:`False`

. The server-side default is :data:`True`

. If this table is
not a view, :data:`None`

is returned.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

## Methods

### from_string

`from_string(full_table_id: str) -> google.cloud.bigquery.table.TableListItem`


Construct a table from fully-qualified table ID.

Parameter |
|
|---|---|
Name |
Description |
`full_table_id` |
`str`
A fully-qualified table ID in standard SQL format. Must included a project ID, dataset ID, and table ID, each separated by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `full_table_id` is not a fully-qualified table ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`Table .. rubric:: Examples >>> Table.from_string('my-project.mydataset.mytable') Table(TableRef...(D...('my-project', 'mydataset'), 'mytable'))` |
Table parsed from `full_table_id` . |

### to_api_repr

`to_api_repr() -> dict`


Constructs the API resource of this table

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Table represented as an API resource |

### to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

Returns |
|
|---|---|
Type |
Description |
`str` |
A reference to this table in the BigQuery Storage API. |
