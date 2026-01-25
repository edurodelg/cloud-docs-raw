---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest
fetched_at: 2026-01-25T02:14:10.220696
---

# Class PatchModelRequest (3.40.0)


      
      Save and categorize content based on your preferences.

`PatchModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the model to patch. |
`dataset_id` |
`str`
Required. Dataset ID of the model to patch. |
`model_id` |
`str`
Required. Model ID of the model to patch. |
`model` |
Required. Patched model. Follows RFC5789 patch semantics. Missing fields are not updated. To clear a field, explicitly set to default value. |