---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem
fetched_at: 2026-01-25T02:12:02.555409
---

# Class TableListItem (3.40.0)


      
      Save and categorize content based on your preferences.

`TableListItem(resource)`


A read-only table resource from a list operation.

For performance reasons, the BigQuery API only includes some of the table properties when listing tables. Notably, xref_schema and xref_num_rows are missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for tables.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list>
```

_.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
A table-like resource object from a table list response. A |

## Properties

### clustering_fields

Union[List[str], None]: Fields defining clustering for the table

(Defaults to :data:`None`

).

Clustering fields are immutable after table creation.

### created

Union[datetime.datetime, None]: Datetime at which the table was
created (:data:`None`

until set from the server).

### expires

Union[datetime.datetime, None]: Datetime at which the table will be deleted.

### friendly_name

Union[str, None]: Title of the table (defaults to :data:`None`

).

### full_table_id

Union[str, None]: ID for the table (:data:`None`

until set from the
server).

In the format `project_id:dataset_id.table_id`

.

### labels

Dict[str, str]: Labels for the table.

This method always returns a dict. To change a table's labels,
modify the dict, then call `Client.update_table`

. To delete a
label, set its value to :data:`None`

before updating.

### partition_expiration

Union[int, None]: Expiration time in milliseconds for a partition.

If this property is set and `type_`

is not set, `type_`

will default to `TimePartitioningType.DAY`

.

### partitioning_type

Union[str, None]: Time partitioning of the table if it is
partitioned (Defaults to :data:`None`

).

### reference

A xref_TableReference pointing to this table.

Returns |
|
|---|---|
Type |
Description |
|
pointer to this table. |

### table_type

Union[str, None]: The type of the table (:data:`None`

until set from
the server).

Possible values are `'TABLE'`

, `'VIEW'`

, or `'EXTERNAL'`

.

### time_partitioning

[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning): Configures time-based
partitioning for a table.

### view_use_legacy_sql

bool: Specifies whether to execute the view with Legacy or Standard SQL.

This boolean specifies whether to execute the view with Legacy SQL
(:data:`True`

) or Standard SQL (:data:`False`

). The client side default is
:data:`False`

. The server-side default is :data:`True`

. If this table is
not a view, :data:`None`

is returned.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

## Methods

### from_string

`from_string(full_table_id: str) -> google.cloud.bigquery.table.TableListItem`


Construct a table from fully-qualified table ID.

Parameter |
|
|---|---|
Name |
Description |
`full_table_id` |
`str`
A fully-qualified table ID in standard SQL format. Must included a project ID, dataset ID, and table ID, each separated by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `full_table_id` is not a fully-qualified table ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`Table .. rubric:: Examples >>> Table.from_string('my-project.mydataset.mytable') Table(TableRef...(D...('my-project', 'mydataset'), 'mytable'))` |
Table parsed from `full_table_id` . |

### to_api_repr

`to_api_repr() -> dict`


Constructs the API resource of this table

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Table represented as an API resource |

### to_bqstorage

`to_bqstorage() -> str`


Construct a BigQuery Storage API representation of this table.

Returns |
|
|---|---|
Type |
Description |
`str` |
A reference to this table in the BigQuery Storage API. |