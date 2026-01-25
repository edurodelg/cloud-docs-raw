---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference
fetched_at: 2026-01-25T02:14:07.929313
---

# Class ModelReference (3.40.0)


      
      Save and categorize content based on your preferences.

`ModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Id path of a model.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. The ID of the project containing this model. |
`dataset_id` |
`str`
Required. The ID of the dataset containing this model. |
`model_id` |
`str`
Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_). The maximum length is 1,024 characters. |