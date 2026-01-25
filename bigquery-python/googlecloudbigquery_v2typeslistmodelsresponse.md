---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse
fetched_at: 2026-01-25T03:18:39.616037
---

# Class ListModelsResponse (3.40.0)


      
      Save and categorize content based on your preferences.

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`models` |
`Sequence[`
Models in the requested dataset. Only the following fields are populated: model_reference, model_type, creation_time, last_modified_time and labels. |
`next_page_token` |
`str`
A token to request the next page of results. |