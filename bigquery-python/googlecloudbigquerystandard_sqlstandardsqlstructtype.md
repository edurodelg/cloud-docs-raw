---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType
fetched_at: 2026-01-25T02:11:23.536485
---

# Class StandardSqlStructType (3.40.0)


      
      Save and categorize content based on your preferences.

```
StandardSqlStructType(
fields: typing.Optional[
typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField]
] = None,
)
```


Type of a struct field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType)

## Parameter |
|
|---|---|
Name |
Description |
`fields` |
`typing.Optional[typing.Iterable[`
The fields in this struct. |

## Properties

### fields

The fields in this struct.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlStructType
```


Construct an SQL struct type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL struct type.