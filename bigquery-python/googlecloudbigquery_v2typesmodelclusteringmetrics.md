---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics
fetched_at: 2026-01-25T03:19:00.945988
---

# Class ClusteringMetrics (3.40.0)


      
      Save and categorize content based on your preferences.

`ClusteringMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics for clustering models.

## Attributes |
|
|---|---|
Name |
Description |
`davies_bouldin_index` |
`google.protobuf.wrappers_pb2.DoubleValue`
Davies-Bouldin index. |
`mean_squared_distance` |
`google.protobuf.wrappers_pb2.DoubleValue`
Mean of squared distances between each sample to its cluster centroid. |
`clusters` |
`Sequence[`
Information for all clusters. |

## Classes

### Cluster

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.