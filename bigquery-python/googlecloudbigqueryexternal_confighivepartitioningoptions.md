---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions
fetched_at: 2026-01-25T02:08:03.822811
---

# Class HivePartitioningOptions (3.40.0)


      
      Save and categorize content based on your preferences.

`HivePartitioningOptions()`


Options that configure hive partitioning.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions)

## Properties

### mode

Optional[str]: When set, what mode of hive partitioning to use when reading data.

Two modes are supported: "AUTO" and "STRINGS".

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode)

### require_partition_filter

Optional[bool]: If set to true, queries over the partitioned table require a partition filter that can be used for partition elimination to be specified.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode)

### source_uri_prefix

Optional[str]: When hive partition detection is requested, a common prefix for all source URIs is required.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.HivePartitioningOptions
```


Factory: construct a `.external_config.HivePartitioningOptions`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
`HivePartitioningOptions` |
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, Any]` |
A dictionary in the format used by the BigQuery API. |