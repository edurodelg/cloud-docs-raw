---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitResult
fetched_at: 2026-01-25T02:12:59.956991
---

# Class DataSplitResult (3.40.0)


      
      Save and categorize content based on your preferences.

`DataSplitResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data split result. This contains references to the training and evaluation data tables that were used to train the model.

## Attributes |
|
|---|---|
Name |
Description |
`training_table` |
Table reference of the training data after split. |
`evaluation_table` |
Table reference of the evaluation data after split. |