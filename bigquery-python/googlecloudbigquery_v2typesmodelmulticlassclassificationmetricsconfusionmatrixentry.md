---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Entry
fetched_at: 2026-01-25T02:13:35.253311
---

# Class Entry (3.40.0)


      
      Save and categorize content based on your preferences.

`Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single entry in the confusion matrix.

## Attributes |
|
|---|---|
Name |
Description |
`predicted_label` |
`str`
The predicted label. For confidence_threshold > 0, we will also add an entry indicating the number of items under the confidence threshold. |
`item_count` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of items being predicted as this label. |