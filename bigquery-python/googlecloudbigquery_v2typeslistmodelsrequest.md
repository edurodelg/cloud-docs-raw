---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest
fetched_at: 2026-01-25T02:12:20.526074
---

# Class ListModelsRequest (3.40.0)


      
      Save and categorize content based on your preferences.

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the models to list. |
`dataset_id` |
`str`
Required. Dataset ID of the models to list. |
`max_results` |
`google.protobuf.wrappers_pb2.UInt32Value`
The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection. |
`page_token` |
`str`
Page token, returned by a previous call to request the next page of results |