---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table
fetched_at: 2026-02-04T00:38:27.959200
---

# Class Table (3.40.0)

`Table(table_ref, schema=None)`


Tables represent a set of rows whose values correspond to a schema.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource-table](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource-table)

## Parameters |
|
|---|---|
Name |
Description |
`table_ref` |
`Union[`
A pointer to a table. If |
`schema` |
`Optional[Sequence[Union[ `
The table's schema. If any item is a mapping, its content must be compatible with |

## Properties

### biglake_configuration

[google.cloud.bigquery.table.BigLakeConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration): Configuration
for managed tables for Apache Iceberg.

See [https://cloud.google.com/bigquery/docs/iceberg-tables](https://cloud.google.com/bigquery/docs/iceberg-tables) for more information.

### clone_definition

Information about the clone. This value is set via clone creation.

See: [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.clone_definition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.clone_definition)

### clustering_fields

Union[List[str], None]: Fields defining clustering for the table

(Defaults to :data:`None`

).

Clustering fields are immutable after table creation.

### created

Union[datetime.datetime, None]: Datetime at which the table was
created (:data:`None`

until set from the server).

### description

Union[str, None]: Description of the table (defaults to
:data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

### encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

See ```
protecting data with Cloud KMS keys
<
```

_
in the BigQuery documentation.[https://cloud.google.com/bigquery/docs/customer-managed-encryption>](https://cloud.google.com/bigquery/docs/customer-managed-encryption>);

### etag

Union[str, None]: ETag for the table resource (:data:`None`

until
set from the server).

### expires

Union[datetime.datetime, None]: Datetime at which the table will be deleted.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

### external_catalog_table_options

Options defining open source compatible datasets living in the BigQuery catalog. Contains metadata of open source database, schema or namespace represented by the current dataset.

### external_data_configuration

Union[google.cloud.bigquery.ExternalConfig, None]: Configuration for
an external data source (defaults to :data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

### foreign_type_info

Optional. Specifies metadata of the foreign data type definition in field schema (TableFieldSchema.foreign_type_definition).

Returns |
|
|---|---|
Type |
Description |
`Optional[schema.ForeignTypeInfo] .. Note:: foreign_type_info is only required if you are referencing an external catalog such as a Hive table. For details, see: https://cloud.google.com/bigquery/docs/external-tables https://cloud.google.com/bigquery/docs/datasets-intro#external_datasets` |
Foreign type information, or :data:`None` if not set. |

### friendly_name

Union[str, None]: Title of the table (defaults to :data:`None`

).

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

### full_table_id

Union[str, None]: ID for the table (:data:`None`

until set from the
server).

In the format `project-id:dataset_id.table_id`

.

### labels

Dict[str, str]: Labels for the table.

This method always returns a dict. To change a table's labels,
modify the dict, then call `Client.update_table`

. To delete a
label, set its value to :data:`None`

before updating.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `value` type is invalid. |

### location

Union[str, None]: Location in which the table is hosted

Defaults to :data:`None`

.

### max_staleness

Union[str, None]: The maximum staleness of data that could be returned when the table is queried.

Staleness encoded as a string encoding of sql IntervalValue type. This property is optional and defaults to None.

According to the BigQuery API documentation, maxStaleness specifies the maximum time interval for which stale data can be returned when querying the table. It helps control data freshness in scenarios like metadata-cached external tables.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
A string representing the maximum staleness interval (e.g., '1h', '30m', '15s' for hours, minutes, seconds respectively). |

### modified

Union[datetime.datetime, None]: Datetime at which the table was last
modified (:data:`None`

until set from the server).

### mview_allow_non_incremental_definition

Optional[bool]: This option declares the intention to construct a
materialized view that isn't refreshed incrementally.
The default value is :data:`False`

.

### mview_enable_refresh

Optional[bool]: Enable automatic refresh of the materialized view
when the base table is updated. The default value is :data:`True`

.

### mview_last_refresh_time

Optional[datetime.datetime]: Datetime at which the materialized view was last
refreshed (:data:`None`

until set from the server).

### mview_query

Optional[str]: SQL query defining the table as a materialized
view (defaults to :data:`None`

).

### mview_refresh_interval

Optional[datetime.timedelta]: The maximum frequency at which this materialized view will be refreshed. The default value is 1800000 milliseconds (30 minutes).

### num_bytes

Union[int, None]: The size of the table in bytes (:data:`None`

until
set from the server).

### num_rows

Union[int, None]: The number of rows in the table (:data:`None`

until set from the server).

### partition_expiration

Union[int, None]: Expiration time in milliseconds for a partition.

If `partition_expiration`

is set and `type_`

is
not set, `type_`

will default to
[DAY](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType).

### partitioning_type

Union[str, None]: Time partitioning of the table if it is
partitioned (Defaults to :data:`None`

).

### range_partitioning

Optional[[google.cloud.bigquery.table.RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)]:
Configures range-based partitioning for a table.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### reference

A xref_TableReference pointing to this table.

Returns |
|
|---|---|
Type |
Description |
|
pointer to this table. |

### require_partition_filter

bool: If set to true, queries over the partitioned table require a partition filter that can be used for partition elimination to be specified.

### resource_tags

Dict[str, str]: Resource tags for the table.

See: [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.resource_tags](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.resource_tags)

### schema

Sequence[Union[ xref_SchemaField, Mapping[str, Any] ]]: Table's schema.

Exceptions |
|
|---|---|
Type |
Description |
`Exception` |
If `schema` is not a sequence, or if any item in the sequence is not a
|

### self_link

Union[str, None]: URL for the table resource (:data:`None`

until set
from the server).

### snapshot_definition

Information about the snapshot. This value is set via snapshot creation.

See: [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.snapshot_definition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.snapshot_definition)

### streaming_buffer

google.cloud.bigquery.StreamingBuffer: Information about a table's streaming buffer.

### table_constraints

Tables Primary Key and Foreign Key information.

### table_type

Union[str, None]: The type of the table (:data:`None`

until set from
the server).

Possible values are `'TABLE'`

, `'VIEW'`

, `'MATERIALIZED_VIEW'`

or
`'EXTERNAL'`

.

### time_partitioning

Optional[[google.cloud.bigquery.table.TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)]: Configures time-based
partitioning for a table.

Only specify at most one of xref_time_partitioning or xref_range_partitioning.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### view_query

Union[str, None]: SQL query defining the table as a view (defaults
to :data:`None`

).

By default, the query is treated as Standard SQL. To use Legacy
SQL, set `view_use_legacy_sql`

to :data:`True`

.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
For invalid value types. |

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

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.table.Table`


Factory: construct a table given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Table resource representation from the API |

Exceptions |
|
|---|---|
Type |
Description |
`KeyError` |
If the `resource` lacks the key `'tableReference'` , or if the `dict` stored within the key `'tableReference'` lacks the keys `'tableId'` , `'projectId'` , or `'datasetId'` . |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.table.Table` |
Table parsed from `resource` . |

### from_string

`from_string(full_table_id: str) -> google.cloud.bigquery.table.Table`


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