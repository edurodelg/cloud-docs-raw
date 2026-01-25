---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table
fetched_at: 2026-01-25T02:11:29.439757
---

# Module table (3.40.0)


      
      Save and categorize content based on your preferences.

Define API Tables.

## Classes

[BigLakeConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.BigLakeConfiguration)

```
BigLakeConfiguration(
connection_id: typing.Optional[str] = None,
storage_uri: typing.Optional[str] = None,
file_format: typing.Optional[str] = None,
table_format: typing.Optional[str] = None,
_properties: typing.Optional[dict] = None,
)
```


Configuration for managed tables for Apache Iceberg, formerly known as BigLake.

Parameters |
|
|---|---|
Name |
Description |
`connection_id` |
`Optional[str]`
The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage. The connection_id can have the form |
`storage_uri` |
`Optional[str]`
The fully qualified location prefix of the external folder where table data is stored. The '*' wildcard character is not allowed. The URI should be in the format |
`file_format` |
`Optional[str]`
The file format the table data is stored in. See BigLakeFileFormat for available values. |
`table_format` |
`Optional[str]`
The table format the metadata only snapshots are stored in. See BigLakeTableFormat for available values. |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

[CloneDefinition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.CloneDefinition)

`CloneDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and clone time of the clone.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#clonedefinition)

[ColumnReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ColumnReference)

`ColumnReference(referencing_column: str, referenced_column: str)`


The pair of the foreign key column and primary key column.

[ForeignKey](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey)

```
ForeignKey(
name: str,
referenced_table: google.cloud.bigquery.table.TableReference,
column_references: typing.List[google.cloud.bigquery.table.ColumnReference],
)
```


Represents a foreign key constraint on a table's columns.

[PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange)

`PartitionRange(start=None, end=None, interval=None, _properties=None)`


Definition of the ranges for range partitioning.

Parameters |
|
|---|---|
Name |
Description |
`start` |
`Optional[int]`
Sets the |
`end` |
`Optional[int]`
Sets the |
`interval` |
`Optional[int]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

[PrimaryKey](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PrimaryKey)

`PrimaryKey(columns: typing.List[str])`


Represents the primary key constraint on a table's columns.

[RangePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning)

`RangePartitioning(range_=None, field=None, _properties=None)`


Range-based partitioning configuration for a table.

Parameters |
|
|---|---|
Name |
Description |
`range_` |
`Optional[`
Sets the range_ property. |
`field` |
`Optional[str]`
Sets the |
`_properties` |
`Optional[dict]`
Private. Used to construct object from API resource. |

[Row](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row)

`Row(values, field_to_index)`


A BigQuery row.

Values can be accessed by position (index), by key like a dict, or as properties.

Parameters |
|
|---|---|
Name |
Description |
`values` |
`Sequence[object]`
The row values |
`field_to_index` |
`Dict[str, int]`
A mapping from schema field names to indexes |

[RowIterator](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator)

```
RowIterator(
client,
api_request,
path,
schema,
page_token=None,
max_results=None,
page_size=None,
extra_params=None,
table=None,
selected_fields=None,
total_rows=None,
first_page_response=None,
location: typing.Optional[str] = None,
job_id: typing.Optional[str] = None,
query_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
num_dml_affected_rows: typing.Optional[int] = None,
query: typing.Optional[str] = None,
total_bytes_processed: typing.Optional[int] = None,
slot_millis: typing.Optional[int] = None,
created: typing.Optional[datetime.datetime] = None,
started: typing.Optional[datetime.datetime] = None,
ended: typing.Optional[datetime.datetime] = None,
)
```


A class for iterating through HTTP/JSON API row list responses.

Parameters |
|
|---|---|
Name |
Description |
`query` |
`Optional[str]`
The query text used. |
`total_bytes_processed` |
`Optional[int]`
If representing query results, the total bytes processed by the associated query. |
`slot_millis` |
`Optional[int]`
If representing query results, the number of slot ms billed for the associated query. |
`created` |
`Optional[datetime.datetime]`
If representing query results, the creation time of the associated query. |
`started` |
`Optional[datetime.datetime]`
If representing query results, the start time of the associated query. |
`ended` |
`Optional[datetime.datetime]`
If representing query results, the end time of the associated query. |
`client` |
`Optional[google.cloud.bigquery.Client]`
The API client instance. This should always be non- |
`api_request` |
`Callable[google.cloud._http.JSONConnection.api_request]`
The function to use to make API requests. |
`path` |
`str`
The method path to query for the list of items. |
`schema` |
`Sequence[Union[ `
The table's schema. If any item is a mapping, its content must be compatible with |
`page_token` |
`str`
A token identifying a page in a result set to start fetching results from. |
`max_results` |
`Optional[int]`
The maximum number of results to fetch. |
`page_size` |
`Optional[int]`
The maximum number of rows in each page of results from this request. Non-positive values are ignored. Defaults to a sensible value set by the API. |
`extra_params` |
`Optional[Dict[str, object]]`
Extra query string parameters for the API call. |
`table` |
`Optional[Union[ `
The table which these rows belong to, or a reference to it. Used to call the BigQuery Storage API to fetch rows. |
`selected_fields` |
`Optional[Sequence[`
A subset of columns to select from this table. |
`total_rows` |
`Optional[int]`
Total number of rows in the table. |
`first_page_response` |
`Optional[dict]`
API response for the first page of results. These are returned when the first page is requested. |

[SnapshotDefinition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.SnapshotDefinition)

`SnapshotDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and snapshot time of the snapshot.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition)

[StreamingBuffer](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.StreamingBuffer)

`StreamingBuffer(resource)`


Information about a table's streaming buffer.

See [https://cloud.google.com/bigquery/streaming-data-into-bigquery](https://cloud.google.com/bigquery/streaming-data-into-bigquery).

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
streaming buffer representation returned from the API |

[Table](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table)

`Table(table_ref, schema=None)`


Tables represent a set of rows whose values correspond to a schema.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource-table](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource-table)

Parameters |
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

[TableConstraints](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints)

```
TableConstraints(
primary_key: typing.Optional[google.cloud.bigquery.table.PrimaryKey],
foreign_keys: typing.Optional[typing.List[google.cloud.bigquery.table.ForeignKey]],
)
```


The TableConstraints defines the primary key and foreign key.

[TableListItem](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem)

`TableListItem(resource)`


A read-only table resource from a list operation.

For performance reasons, the BigQuery API only includes some of the table properties when listing tables. Notably, xref_schema and xref_num_rows are missing.

For a full list of the properties that the BigQuery API returns, see the
```
REST documentation for tables.list
<https://cloud.google.com/bigquery/docs/reference/rest/v2/tables/list>
```

_.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
A table-like resource object from a table list response. A |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `tableReference` or one of its required members is missing from `resource` . |

[TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)

`TableReference(dataset_ref: DatasetReference, table_id: str)`


TableReferences are pointers to tables.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#tablereference)

[TimePartitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioning)

```
TimePartitioning(
type_=None, field=None, expiration_ms=None, require_partition_filter=None
)
```


Configures time-based partitioning for a table.

Parameters |
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

[TimePartitioningType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TimePartitioningType)

`TimePartitioningType()`


Specifies the type of time partitioning to perform.