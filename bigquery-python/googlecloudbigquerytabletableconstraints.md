---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints
fetched_at: 2026-01-25T02:12:00.431058
---

# Class TableConstraints (3.40.0)


      
      Save and categorize content based on your preferences.

```
TableConstraints(
primary_key: typing.Optional[google.cloud.bigquery.table.PrimaryKey],
foreign_keys: typing.Optional[typing.List[google.cloud.bigquery.table.ForeignKey]],
)
```


The TableConstraints defines the primary key and foreign key.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.table.TableConstraints
```


Create an instance from API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Return a dictionary representing this object.