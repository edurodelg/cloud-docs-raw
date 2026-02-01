---
merged_at: 2026-02-01T08:10:00.335675
merged_files: 2
---


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/format_options -->

# BigQuery Format Options

*class* google.cloud.bigquery.format_options.AvroOptions()

Options if source format is set to AVRO.

*classmethod* from_api_repr(resource: [Dict](https://docs.python.org/3/library/typing.html#typing.Dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [bool](https://docs.python.org/3/library/functions.html#bool)])

Factory: construct an instance from a resource dict.

**Parameters****resource**(*Dict**[**str**, *[*bool*](*]*) – Definition of a[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool))`AvroOptions`

instance in the same representation as is returned from the API.**Returns**Configuration parsed from

`resource`

.**Return type**`AvroOptions`


#### to_api_repr()

Build an API representation of this object.

*property* use_avro_logical_types(*: Optional[*[bool](https://docs.python.org/3/library/functions.html#bool) )

[bool](https://docs.python.org/3/library/functions.html#bool)

[Optional] If sourceFormat is set to ‘AVRO’, indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

*class* google.cloud.bigquery.format_options.ParquetOptions()

Additional options if the PARQUET source format is used.

*property* enable_list_inference(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

Indicates whether to use schema inference specifically for Parquet LIST logical type.

*property* enum_as_string(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string)

*classmethod* from_api_repr(resource: [Dict](https://docs.python.org/3/library/typing.html#typing.Dict)[[str](https://docs.python.org/3/library/stdtypes.html#str), [bool](https://docs.python.org/3/library/functions.html#bool)])

Factory: construct an instance from a resource dict.

**Parameters****resource**(*Dict**[**str**, *[*bool*](*]*) – Definition of a[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool))`ParquetOptions`

instance in the same representation as is returned from the API.**Returns**Configuration parsed from

`resource`

.**Return type**`ParquetOptions`


*property* map_target_type(*: Optional[Union[*[bool](https://docs.python.org/3/library/functions.html#bool), [str](https://docs.python.org/3/library/stdtypes.html#str)] )

[bool](https://docs.python.org/3/library/functions.html#bool),

[str](https://docs.python.org/3/library/stdtypes.html#str)]

Indicates whether to simplify the representation of parquet maps to only show keys and values.

#### to_api_repr()

Build an API representation of this object.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaModelInfo -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch -->

# Class SourceColumnMatch (3.40.0)

`SourceColumnMatch(value)`


Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Error -->

# Class Error (3.40.0)

Exception representing all non-warning DB-API errors.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DatabaseError -->

# Class DatabaseError (3.40.0)

DB-API error related to the database.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats -->

# Class DmlStats (3.40.0)

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Detailed statistics for DML statements.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats](https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats)

## Methods

### DmlStats

```
DmlStats(
inserted_row_count: int = 0, deleted_row_count: int = 0, updated_row_count: int = 0
)
```


Create new instance of DmlStats(inserted_row_count, deleted_row_count, updated_row_count)

### count

`count(value, /)`


Return number of occurrences of value.

### index

`index(value, start=0, stop=9223372036854775807, /)`


Return first index of value.

Raises ValueError if the value is not present.
