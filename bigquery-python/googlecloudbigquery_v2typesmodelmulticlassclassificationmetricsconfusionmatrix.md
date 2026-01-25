---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix
fetched_at: 2026-01-25T03:19:50.644675
---

# Class ConfusionMatrix (3.40.0)


      
      Save and categorize content based on your preferences.

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Confidence threshold used when computing the entries of the confusion matrix. |
`rows` |
`Sequence[`
One row per actual label. |

## Classes

### Entry

`Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single entry in the confusion matrix.

### Row

`Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single row in the confusion matrix.