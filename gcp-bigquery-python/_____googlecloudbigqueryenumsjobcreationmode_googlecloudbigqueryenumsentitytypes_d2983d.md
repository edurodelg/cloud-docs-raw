---
merged_at: 2026-01-26T23:27:21.518190
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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode -->

# Class JobCreationMode (3.40.0)

`JobCreationMode()`


Documented values for Job Creation Mode.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.EntityTypes -->

# Class EntityTypes (3.40.0)

`EntityTypes(value)`


Enum of allowed entity type names in AccessEntry

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LossType -->

# Class LossType (3.40.0)

`LossType(value)`


Loss metric to evaluate model training performance.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.NotSupportedError -->

# Class NotSupportedError (3.40.0)

DB-API error for operations not supported by the database or API.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaOrder -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes -->

# Class DefaultPandasDTypes (3.40.0)

`DefaultPandasDTypes(value)`


Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty -->

# Class ConnectionProperty (3.40.0)

`ConnectionProperty(key: str = "", value: str = "")`


A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

## Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the property to set, for example, |
`value` |
`str`
The value of the property to set. |

## Properties

### key

Name of the property.

For example:

`time_zone`

`session_id`


### value

Value of the property.

## Methods

### from_api_repr

`from_api_repr(resource) -> google.cloud.bigquery.query.ConnectionProperty`


Construct xref_ConnectionProperty from JSON resource.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct JSON API representation for the connection property.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry -->

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
