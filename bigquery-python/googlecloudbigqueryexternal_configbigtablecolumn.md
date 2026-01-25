---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumn
fetched_at: 2026-01-25T03:13:52.019415
---

# Class BigtableColumn (3.40.0)


      
      Save and categorize content based on your preferences.

`BigtableColumn()`


Options for a Bigtable column.

## Properties

### encoding

str: The encoding of the values when the type is not `STRING`


See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.encoding)

### field_name

str: An identifier to use if the qualifier is not a valid BigQuery field identifier

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.field_name](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.field_name)

### only_read_latest

bool: If this is set, only the latest version of value in this column are exposed.

### qualifier_encoded

Union[str, bytes]: The qualifier encoded in binary.

The type is `str`

(Python 2.x) or `bytes`

(Python 3.x). The module
will handle base64 encoding for you.

### qualifier_string

str: A valid UTF-8 string qualifier

### type_

str: The type to convert the value in cells of this column.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumn.FIELDS.type)

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumn
```


Factory: construct a `.external_config.BigtableColumn`

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
`external_config.BigtableColumn` |
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