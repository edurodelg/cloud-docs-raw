---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.EvaluationMetrics
fetched_at: 2026-01-25T03:19:22.942812
---

# Class EvaluationMetrics (3.40.0)


      
      Save and categorize content based on your preferences.

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