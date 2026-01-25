---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model
fetched_at: 2026-01-25T02:12:25.002090
---

# Class Model (3.40.0)


      
      Save and categorize content based on your preferences.

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