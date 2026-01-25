---
merged_at: 2026-01-25T15:38:56.573768
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelarimaforecastingmetricsarimasinglemodelforecas_29d6c8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelarimaforecastingmetricsarimasinglemodelforecast_e6425e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelarimaforecastingmetricsarimasinglemodelforecastingmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaForecastingMetrics.ArimaSingleModelForecastingMetrics -->

# Class ArimaSingleModelForecastingMetrics (3.40.0)

```
ArimaSingleModelForecastingMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Model evaluation metrics for a single ARIMA forecasting model.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
Non-seasonal order. |
`arima_fitting_metrics` |
Arima fitting metrics. |
`has_drift` |
`bool`
Is arima model fitted with drift or not. It is always false when d is not 1. |
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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytablepartitionrange_googlecloudbigquerytabletableconstraints.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablepartitionrange.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange -->

# Class PartitionRange (3.40.0)

`PartitionRange(start=None, end=None, interval=None, _properties=None)`


Definition of the ranges for range partitioning.

## Parameters |
|
|---|---|
Name |
Description |
`start` |
`Optional[int]`
Sets the |
`end` |
`Optional[int]`
Sets the |
`interval` |
`Optional[int]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### end

int: The end of range partitioning, exclusive.

### interval

int: The width of each interval.

### start

int: The start of range partitioning, inclusive.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytabletableconstraints.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints -->

# Class TableConstraints (3.40.0)

```
TableConstraints(
primary_key: typing.Optional[google.cloud.bigquery.table.PrimaryKey],
foreign_keys: typing.Optional[typing.List[google.cloud.bigquery.table.ForeignKey]],
)
```


The TableConstraints defines the primary key and foreign key.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.TableConstraints
```


Create an instance from API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryretry_googlecloudbigquerydbapiwarning_googlecloudbigqueryj_d1c57f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryretry_googlecloudbigquerydbapiwarning_googlecloudbigqueryjo_af2d9e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryretry_googlecloudbigquerydbapiwarning.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryretry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.retry -->

# Module retry (3.40.0)

API documentation for `bigquery.retry`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapiwarning.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Warning -->

# Class Warning (3.40.0)

Exception raised for important DB-API warnings.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobbasescriptstatistics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typeslistmodelsrequest_googlecloudbigquerystandard_sqlsta_ac51fe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typeslistmodelsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest -->

# Class ListModelsRequest (3.40.0)

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the models to list. |
`dataset_id` |
`str`
Required. Dataset ID of the models to list. |
`max_results` |
`google.protobuf.wrappers_pb2.UInt32Value`
The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection. |
`page_token` |
`str`
Page token, returned by a previous call to request the next page of results |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerystandard_sqlstandardsqltabletype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType -->

# Class StandardSqlTableType (3.40.0)

```
StandardSqlTableType(
columns: typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField],
)
```


A table type.

## Properties

### columns

The columns in this table type.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlTableType
```


Construct an SQL table type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL table type.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobqueryplanentry___googlecloudbigquery_v2typesmodelmulticla_d81806.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobqueryplanentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry -->

# Class QueryPlanEntry (3.40.0)

`QueryPlanEntry()`


QueryPlanEntry represents a single stage of a query execution plan.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage)
for the underlying API representation within query statistics.

## Properties

### completed_parallel_inputs

Optional[int]: Number of parallel input segments completed.

### compute_ms_avg

Optional[int]: Milliseconds the average worker spent on CPU-bound processing.

### compute_ms_max

Optional[int]: Milliseconds the slowest worker spent on CPU-bound processing.

### compute_ratio_avg

Optional[float]: Ratio of time the average worker spent on CPU-bound processing, relative to the longest time spent by any worker in any stage of the overall plan.

### compute_ratio_max

Optional[float]: Ratio of time the slowest worker spent on CPU-bound processing, relative to the longest time spent by any worker in any stage of the overall plan.

### end

Optional[Datetime]: Datetime when the stage ended.

### entry_id

Optional[str]: Unique ID for the stage within the plan.

### input_stages

List(int): Entry IDs for stages that were inputs for this stage.

### name

Optional[str]: Human-readable name of the stage.

### parallel_inputs

Optional[int]: Number of parallel input segments within the stage.

### read_ms_avg

Optional[int]: Milliseconds the average worker spent reading input.

### read_ms_max

Optional[int]: Milliseconds the slowest worker spent reading input.

### read_ratio_avg

Optional[float]: Ratio of time the average worker spent reading input, relative to the longest time spent by any worker in any stage of the overall plan.

### read_ratio_max

Optional[float]: Ratio of time the slowest worker spent reading to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

### records_read

Optional[int]: Number of records read by this stage.

### records_written

Optional[int]: Number of records written by this stage.

### shuffle_output_bytes

Optional[int]: Number of bytes written by this stage to intermediate shuffle.

### shuffle_output_bytes_spilled

Optional[int]: Number of bytes written by this stage to intermediate shuffle and spilled to disk.

### slot_ms

Optional[int]: Slot-milliseconds used by the stage.

### start

Optional[Datetime]: Datetime when the stage started.

### status

Optional[str]: status of this stage.

### steps

List(QueryPlanEntryStep): List of step operations performed by each worker in the stage.

### wait_ms_avg

Optional[int]: Milliseconds the average worker spent waiting to be scheduled.

### wait_ms_max

Optional[int]: Milliseconds the slowest worker spent waiting to be scheduled.

### wait_ratio_avg

Optional[float]: Ratio of time the average worker spent waiting to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

### wait_ratio_max

Optional[float]: Ratio of time the slowest worker spent waiting to be scheduled, relative to the longest time spent by any worker in any stage of the overall plan.

### write_ms_avg

Optional[int]: Milliseconds the average worker spent writing output data.

### write_ms_max

Optional[int]: Milliseconds the slowest worker spent writing output data.

### write_ratio_avg

Optional[float]: Ratio of time the average worker spent writing output data, relative to the longest time spent by any worker in any stage of the overall plan.

### write_ratio_max

Optional[float]: Ratio of time the slowest worker spent writing output data, relative to the longest time spent by any worker in any stage of the overall plan.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.job.query.QueryPlanEntry`


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.QueryPlanEntry` |
Query plan entry parsed from `resource` . |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelmulticlassclassificationmetrics_googlecloudbig_4cf847.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelmulticlassclassificationmetrics_googlecloudbigq_f36b42.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelmulticlassclassificationmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics -->

# Class MultiClassClassificationMetrics (3.40.0)

```
MultiClassClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Evaluation metrics for multi-class classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`confusion_matrix_list` |
`Sequence[`
Confusion matrix at different thresholds. |

## Classes

### ConfusionMatrix

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobbasescriptstackframe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame -->

# Class ScriptStackFrame (3.40.0)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablerow.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row -->

# Class Row (3.40.0)

`Row(values, field_to_index)`


A BigQuery row.

Values can be accessed by position (index), by key like a dict, or as properties.

## Parameters |
|
|---|---|
Name |
Description |
`values` |
`Sequence[object]`
The row values |
`field_to_index` |
`Dict[str, int]`
A mapping from schema field names to indexes |

## Methods

### get

`get(key: str, default: typing.Optional[typing.Any] = None) -> typing.Any`


Return a value for key, with a default value if it does not exist.

Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the column to access |
`default` |
`object`
The default value to use if the key does not exist. (Defaults to :data: |

Returns |
|
|---|---|
Type |
Description |
`object .. rubric:: Examples When the key exists, the value associated with it is returned. >>> Row(('a', 'b'), {'x': 0, 'y': 1}).get('x') 'a' The default value is :data:` |
The value associated with the provided key, or a default value. |

### items

`items() -> typing.Iterable[typing.Tuple[str, typing.Any]]`


Return items as `(key, value)`

pairs.

Returns |
|
|---|---|
Type |
Description |
`Iterable[Tuple[str, object]] .. rubric:: Examples >>> list(Row(('a', 'b'), {'x': 0, 'y': 1}).items()) [('x', 'a'), ('y', 'b')]` |
The `(key, value)` pairs representing this row. |

### keys

`keys() -> typing.Iterable[str]`


Return the keys for using a row as a dict.

Returns |
|
|---|---|
Type |
Description |
`Iterable[str] .. rubric:: Examples >>> list(Row(('a', 'b'), {'x': 0, 'y': 1}).keys()) ['x', 'y']` |
The keys corresponding to the columns of a row |

### values

`values()`


Return the values included in this row.

Returns |
|
|---|---|
Type |
Description |
`Sequence[object]` |
A sequence of length `len(row)` . |
