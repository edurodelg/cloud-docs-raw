---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster
fetched_at: 2026-01-25T02:12:45.335633
---

# Class Cluster (3.40.0)


      
      Save and categorize content based on your preferences.

`Cluster(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message containing the information about one cluster.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`feature_values` |
`Sequence[`
Values of highly variant features for this cluster. |
`count` |
`google.protobuf.wrappers_pb2.Int64Value`
Count of training data rows that were assigned to this cluster. |

## Classes

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a single feature within the cluster.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)