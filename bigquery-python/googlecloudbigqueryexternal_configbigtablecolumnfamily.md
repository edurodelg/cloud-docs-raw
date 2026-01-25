---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily
fetched_at: 2026-01-25T02:07:32.790608
---

# Class BigtableColumnFamily (3.40.0)


      
      Save and categorize content based on your preferences.

`BigtableColumnFamily()`


Options for a Bigtable column family.

## Properties

### columns

List[BigtableColumn]: Lists of columns that should be exposed as individual fields.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.columns](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.columns)

### encoding

str: The encoding of the values when the type is not `STRING`


See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.encoding)

### family_id

str: Identifier of the column family.

### only_read_latest

bool: If this is set only the latest version of value are exposed for all columns in this column family.

### type_

str: The type to convert the value in cells of this column family.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.type)

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumnFamily
```


Factory: construct a `.external_config.BigtableColumnFamily`

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
|
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