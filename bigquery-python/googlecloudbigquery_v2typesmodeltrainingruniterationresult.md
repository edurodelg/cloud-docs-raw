---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult
fetched_at: 2026-01-25T03:20:10.964075
---

# Class IterationResult (3.40.0)


      
      Save and categorize content based on your preferences.

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