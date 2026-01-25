---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics
fetched_at: 2026-01-25T03:18:56.534394
---

# Class BinaryClassificationMetrics (3.40.0)


      
      Save and categorize content based on your preferences.

`BinaryClassificationMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for binary classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`binary_confusion_matrix_list` |
`Sequence[`
Binary confusion matrix at multiple thresholds. |
`positive_label` |
`str`
Label representing the positive class. |
`negative_label` |
`str`
Label representing the negative class. |

## Classes

### BinaryConfusionMatrix

`BinaryConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for binary classification models.