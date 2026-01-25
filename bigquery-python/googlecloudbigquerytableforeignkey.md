---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey
fetched_at: 2026-01-25T02:11:38.703392
---

# Class ForeignKey (3.40.0)


      
      Save and categorize content based on your preferences.

```
ForeignKey(
name: str,
referenced_table: google.cloud.bigquery.table.TableReference,
column_references: typing.List[google.cloud.bigquery.table.ColumnReference],
)
```


Represents a foreign key constraint on a table's columns.

## Methods

### from_api_repr

```
from_api_repr(
api_repr: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.ForeignKey
```


Create an instance from API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.