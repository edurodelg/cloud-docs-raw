---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue.CategoryCount
fetched_at: 2026-01-25T03:19:11.244189
---

# Class CategoryCount (3.40.0)


      
      Save and categorize content based on your preferences.

`CategoryCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the count of a single category within the cluster.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
`str`
The name of category. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
The count of training samples matching the category within the cluster. |