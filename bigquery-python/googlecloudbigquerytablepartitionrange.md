---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange
fetched_at: 2026-01-25T03:17:57.758879
---

# Class PartitionRange (3.40.0)


      
      Save and categorize content based on your preferences.

`PartitionRange(start=None, end=None, interval=None, _properties=None)`


Definition of the ranges for range partitioning.

## Parameters |
|
|---|---|
Name |
Description |
`start` |
`Optional[int]`
Sets the |
`end` |
`Optional[int]`
Sets the |
`interval` |
`Optional[int]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

## Properties

### end

int: The end of range partitioning, exclusive.

### interval

int: The width of each interval.

### start

int: The start of range partitioning, inclusive.