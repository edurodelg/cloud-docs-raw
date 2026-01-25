---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning
fetched_at: 2026-01-25T02:11:45.998222
---

# Class RangePartitioning (3.40.0)


      
      Save and categorize content based on your preferences.

`RangePartitioning(range_=None, field=None, _properties=None)`


Range-based partitioning configuration for a table.

## Parameters |
|
|---|---|
Name |
Description |
`range_` |
`Optional[`
Sets the range_ property. |
`field` |
`Optional[str]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### field

str: The table is partitioned by this field.

The field must be a top-level `NULLABLE`

/ `REQUIRED`

field. The
only supported type is `INTEGER`

/ `INT64`

.

### range_

[google.cloud.bigquery.table.PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange): Defines the
ranges for range partitioning.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not a `PartitionRange` . |