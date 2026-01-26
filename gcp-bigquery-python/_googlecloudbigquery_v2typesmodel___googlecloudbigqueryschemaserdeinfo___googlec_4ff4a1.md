---
merged_at: 2026-01-26T21:00:49.241953
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model -->

# Class Model (3.40.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`etag` |
`str`
Output only. A hash of this resource. |
`model_reference` |
Required. Unique identifier for this model. |
`creation_time` |
`int`
Output only. The time when this model was created, in millisecs since the epoch. |
`last_modified_time` |
`int`
Output only. The time when this model was last modified, in millisecs since the epoch. |
`description` |
`str`
Optional. A user-friendly description of this model. |
`friendly_name` |
`str`
Optional. A descriptive name for this model. |
`labels` |
`Mapping[str, str]`
The labels associated with this model. You can use these to organize and group your models. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key. |
`expiration_time` |
`int`
Optional. The time when this model expires, in milliseconds since the epoch. If not present, the model will persist indefinitely. Expired models will be deleted and their storage reclaimed. The defaultTableExpirationMs property of the encapsulating dataset can be used to set a default expirationTime on newly created models. |
`location` |
`str`
Output only. The geographic location where the model resides. This value is inherited from the dataset. |
`encryption_configuration` |
Custom encryption configuration (e.g., Cloud KMS keys). This shows the encryption configuration of the model data while stored in BigQuery storage. This field can be used with PatchModel to update encryption key for an already encrypted model. |
`model_type` |
Output only. Type of the model resource. |
`training_runs` |
`Sequence[`
Output only. Information for all training runs in increasing order of start_time. |
`feature_columns` |
`Sequence[`
Output only. Input feature columns that were used to train this model. |
`label_columns` |
`Sequence[`
Output only. Label columns that were used to train this model. The output of the model will have a `predicted_`
prefix to these columns.
|
`best_trial_id` |
`int`
The best trial_id across all training runs. |

## Classes

### AggregateClassificationMetrics

```
AggregateClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

### ArimaFittingMetrics

`ArimaFittingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ARIMA model fitting metrics.

### ArimaForecastingMetrics

`ArimaForecastingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model evaluation metrics for ARIMA forecasting models.

### ArimaOrder

`ArimaOrder(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima order, can be used for both non-seasonal and seasonal parts.

### BinaryClassificationMetrics

`BinaryClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for binary classification/classifier models.

### ClusteringMetrics

`ClusteringMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for clustering models.

### DataFrequency

`DataFrequency(value)`


Type of supported data frequency for time series forecasting models.

### DataSplitMethod

`DataSplitMethod(value)`


Indicates the method to split input data into multiple tables.

### DataSplitResult

`DataSplitResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data split result. This contains references to the training and evaluation data tables that were used to train the model.

### DistanceType

`DistanceType(value)`


Distance metric used to compute the distance between two points.

### EvaluationMetrics

`EvaluationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics of a model. These are either computed on all training data or just the eval data based on whether eval data was used during training. These are not present for imported models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### FeedbackType

`FeedbackType(value)`


Indicates the training algorithm to use for matrix factorization models.

### GlobalExplanation

`GlobalExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Global explanations containing the top most important features after training.

### HolidayRegion

`HolidayRegion(value)`


Type of supported holiday regions for time series forecasting models.

### KmeansEnums

`KmeansEnums(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.KmeansEnums`

class.

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### LearnRateStrategy

`LearnRateStrategy(value)`


Indicates the learning rate optimization strategy to use.

### LossType

`LossType(value)`


Loss metric to evaluate model training performance.

### ModelType

`ModelType(value)`


Indicates the type of the Model.

### MultiClassClassificationMetrics

```
MultiClassClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Evaluation metrics for multi-class classification/classifier models.

### OptimizationStrategy

`OptimizationStrategy(value)`


Indicates the optimization strategy used for training.

### RankingMetrics

`RankingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

### RegressionMetrics

`RegressionMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for regression and explicit feedback type matrix factorization models.

### SeasonalPeriod

`SeasonalPeriod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod`

class.

### TrainingRun

`TrainingRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single training query run for the model.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel -->

# Class DeterminismLevel (3.40.0)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel -->

# Class DeterminismLevel (3.40.0)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics -->

# Class ArimaFittingMetrics (3.40.0)

`ArimaFittingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ARIMA model fitting metrics.

## Attributes |
|
|---|---|
Name |
Description |
`log_likelihood` |
`float`
Log-likelihood. |
`aic` |
`float`
AIC. |
`variance` |
`float`
Variance. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo -->

# Class SessionInfo (3.40.0)

`SessionInfo(resource)`


[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### session_id

The ID of the session.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/job_base -->

# Common Job Resource Classes

Base classes and helpers for job classes.

*class* google.cloud.bigquery.job.base.ReservationUsage(name, slot_ms)

Job resource usage for a reservation.

Create new instance of ReservationUsage(name, slot_ms)

#### name()

Reservation name or “unreserved” for on-demand resources usage.

#### slot_ms()

Total slot milliseconds used by the reservation for a particular job.

*class* google.cloud.bigquery.job.base.ScriptStackFrame(resource)

Stack frame showing the line/column/procedure name where the current evaluation happened.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* end_column()

One-based end column.

**Type**

*property* end_line()

One-based end line.

**Type**

*property* procedure_id()

Name of the active procedure.

Omitted if in a top-level script.

**Type**Optional[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*property* start_column()

One-based start column.

**Type**

*property* start_line()

One-based start line.

**Type**

*property* text()

Text of the current statement/expression.

**Type**

*class* google.cloud.bigquery.job.base.ScriptStatistics(resource)

Statistics for a child job of a script.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* evaluation_kind(*: Optional[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

**Type**

*property* stack_frames(*: Sequence[google.cloud.bigquery.job.base.ScriptStackFrame* )

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.

*class* google.cloud.bigquery.job.base.SessionInfo(resource)

[Preview] Information of the session if this job is part of one.

**Versionadded:** New in version 2.29.0.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* session_id(*: Optional[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

The ID of the session.

*class* google.cloud.bigquery.job.base.TransactionInfo(transaction_id: [str](https://docs.python.org/3/library/stdtypes.html#str))

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

**Versionadded:** New in version 2.24.0.

Create new instance of TransactionInfo(transaction_id,)

#### transaction_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Output only. ID of the transaction.

*class* google.cloud.bigquery.job.base.UnknownJob(job_id, client)

A job whose type cannot be determined.

*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict), client)

Construct an UnknownJob from the JSON representation.

**Parameters****resource**(*Dict*) – JSON representation of a job.**client**() – Client connected to BigQuery API.*google.cloud.bigquery.client.Client*

**Returns**Job corresponding to the resource.

**Return type**UnknownJob
