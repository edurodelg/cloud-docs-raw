---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics
fetched_at: 2026-01-25T02:13:30.652317
---

# Class MultiClassClassificationMetrics (3.40.0)


      
      Save and categorize content based on your preferences.

```
MultiClassClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Evaluation metrics for multi-class classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`confusion_matrix_list` |
`Sequence[`
Confusion matrix at different thresholds. |

## Classes

### ConfusionMatrix

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.