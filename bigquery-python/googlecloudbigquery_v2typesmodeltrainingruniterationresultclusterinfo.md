---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ClusterInfo
fetched_at: 2026-01-25T02:14:01.631919
---

# Class ClusterInfo (3.40.0)


      
      Save and categorize content based on your preferences.

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`cluster_radius` |
`google.protobuf.wrappers_pb2.DoubleValue`
Cluster radius, the average distance from centroid to each point assigned to the cluster. |
`cluster_size` |
`google.protobuf.wrappers_pb2.Int64Value`
Cluster size, the total number of points assigned to the cluster. |