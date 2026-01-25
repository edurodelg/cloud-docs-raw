---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning
fetched_at: 2026-01-25T03:18:23.038451
---

# Class TimePartitioning (3.40.0)


      
      Save and categorize content based on your preferences.

```
TimePartitioning(
type_=None, field=None, expiration_ms=None, require_partition_filter=None
)
```


Configures time-based partitioning for a table.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Optional[`
Specifies the type of time partitioning to perform. Defaults to |
`field` |
`Optional[str]`
If set, the table is partitioned by this field. If not set, the table is partitioned by pseudo column |
`expiration_ms` |
`Optional[int]`
Number of milliseconds for which to keep the storage for a partition. |
`require_partition_filter` |
`Optional[bool]`
DEPRECATED: Use |

## Properties

### expiration_ms

int: Number of milliseconds to keep the storage for a partition.

### field

str: Field in the table to use for partitioning

### require_partition_filter

bool: Specifies whether partition filters are required for queries

DEPRECATED: Use
[require_partition_filter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table),
instead.

### type_

[google.cloud.bigquery.table.TimePartitioningType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType): The type of time
partitioning to use.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.table.TimePartitioning`


Return a `TimePartitioning`

object deserialized from a dict.

This method creates a new `TimePartitioning`

instance that points to
the `api_repr`

parameter as its internal properties dict. This means
that when a `TimePartitioning`

instance is stored as a property of
another object, any changes made at the higher level will also appear
here::

```
>>> time_partitioning = TimePartitioning()
>>> table.time_partitioning = time_partitioning
>>> table.time_partitioning.field = 'timecolumn'
>>> time_partitioning.field
'timecolumn'
```


Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Mapping[str, str]`
The serialized representation of the TimePartitioning, such as what is output by |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.table.TimePartitioning` |
The `TimePartitioning` object. |

### to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

This method returns the properties dict of the `TimePartitioning`

instance rather than making a copy. This means that when a
`TimePartitioning`

instance is stored as a property of another
object, any changes made at the higher level will also appear here.

Returns |
|
|---|---|
Type |
Description |
`dict` |
A dictionary representing the TimePartitioning object in serialized form. |