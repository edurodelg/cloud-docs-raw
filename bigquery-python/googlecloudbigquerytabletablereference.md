---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference
fetched_at: 2026-01-25T03:18:20.819677
---

# Class TableReference (3.40.0)


      
      Save and categorize content based on your preferences.

`TableReference(dataset_ref: DatasetReference, table_id: str)`


TableReferences are pointers to tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference)

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.table.TableReference`


Factory: construct a table reference given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Table reference representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.table.TableReference` |
Table reference parsed from `resource` . |

### from_string

```
from_string(
table_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.table.TableReference
```


Construct a table reference from table ID string.

Parameters |
|
|---|---|
Name |
Description |
`table_id` |
`str`
A table ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `table_id` is not a fully-qualified table ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`TableReference .. rubric:: Examples >>> TableReference.from_string('my-project.mydataset.mytable') TableRef...(DatasetRef...('my-project', 'mydataset'), 'mytable')` |
Table reference parsed from `table_id` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this table reference.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Table reference represented as an API resource |

### to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

Install the `google-cloud-bigquery-storage`

package to use this
feature.

If the `table_id`

contains a partition identifier (e.g.
`my_table$201812`

) or a snapshot identifier (e.g.
`mytable@1234567890`

), it is ignored. Use
xref_TableReadOptions
to filter rows by partition. Use
xref_TableModifiers
to select a specific snapshot to read from.

Returns |
|
|---|---|
Type |
Description |
`str` |
A reference to this table in the BigQuery Storage API. |