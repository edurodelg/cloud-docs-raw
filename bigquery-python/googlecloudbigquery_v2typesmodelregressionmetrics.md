---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RegressionMetrics
fetched_at: 2026-01-25T03:20:02.086481
---

# Class RegressionMetrics (3.40.0)


      
      Save and categorize content based on your preferences.

`RegressionMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for regression and explicit feedback type matrix factorization models.

## Attributes |
|
|---|---|
Name |
Description |
`mean_absolute_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean absolute error. |
`mean_squared_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean squared error. |
`mean_squared_log_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean squared log error. |
`median_absolute_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Median absolute error. |
`r_squared` |
`google.protobuf.wrappers_pb2.DoubleValue`
R^2 score. This corresponds to r2_score in ML.EVALUATE. |