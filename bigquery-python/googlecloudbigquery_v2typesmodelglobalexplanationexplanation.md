---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation.Explanation
fetched_at: 2026-01-25T02:13:11.265224
---

# Class Explanation (3.40.0)


      
      Save and categorize content based on your preferences.

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`feature_name` |
`str`
Full name of the feature. For non-numerical features, will be formatted like |
`attribution` |
`google.protobuf.wrappers_pb2.DoubleValue`
Attribution of feature. |