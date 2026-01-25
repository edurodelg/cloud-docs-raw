---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ClusteringMetrics.Cluster.FeatureValue.CategoricalValue
fetched_at: 2026-01-25T02:12:49.746507
---

# Class CategoricalValue (3.40.0)


      
      Save and categorize content based on your preferences.

`CategoricalValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Representative value of a categorical feature.

## Attribute |
|
|---|---|
Name |
Description |
`category_counts` |
`Sequence[`
Counts of all categories for the categorical feature. If there are more than ten categories, we return top ten (by count) and return one more CategoryCount with category "*OTHER*" and count as aggregate counts of remaining categories. |

## Classes

### CategoryCount

`CategoryCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the count of a single category within the cluster.