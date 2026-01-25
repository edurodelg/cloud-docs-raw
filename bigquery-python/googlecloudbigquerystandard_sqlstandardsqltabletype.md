---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType
fetched_at: 2026-01-25T03:17:44.007163
---

# Class StandardSqlTableType (3.40.0)


      
      Save and categorize content based on your preferences.

```
StandardSqlTableType(
columns: typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField],
)
```


A table type.

## Properties

### columns

The columns in this table type.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlTableType
```


Construct an SQL table type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL table type.