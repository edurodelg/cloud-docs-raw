---
merged_at: 2026-01-26T21:00:49.250543
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table -->

# Module table (3.40.0)

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

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2types___googlecloudbigquerytablecolumnreference_googleclo_62c800.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types -->

# Package types (3.40.0)

API documentation for `bigquery_v2.types`

package.

## Classes

[DeleteModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest)

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration)

[GetModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest)

[ListModelsRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest)

[ListModelsResponse](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse)

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference)

Id path of a model.

[PatchModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest)

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType)

The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField)

A field or a column.

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType)

A table type


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerytablecolumnreference_googlecloudbigqueryjobcompression__goo_458031.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytablecolumnreference_googlecloudbigqueryjobcompression.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablecolumnreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ColumnReference -->

# Class ColumnReference (3.40.0)

`ColumnReference(referencing_column: str, referenced_column: str)`


The pair of the foreign key column and primary key column.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobcompression.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobdestinationformat_googlecloudbigqueryenumscompression.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobdestinationformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumscompression.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerytablerangepartitioning_googlecloudbigquery_v2typesmodeltrai_ecb4b6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytablerangepartitioning_googlecloudbigquery_v2typesmodeltrain_a24f52.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablerangepartitioning.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RangePartitioning -->

# Class RangePartitioning (3.40.0)

`RangePartitioning(range_=None, field=None, _properties=None)`


Range-based partitioning configuration for a table.

## Parameters |
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

## Properties

### field

str: The table is partitioned by this field.

The field must be a top-level `NULLABLE`

/ `REQUIRED`

field. The
only supported type is `INTEGER`

/ `INT64`

.

### range_

[google.cloud.bigquery.table.PartitionRange](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange): Defines the
ranges for range partitioning.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not a `PartitionRange` . |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeltrainingruniterationresultarimaresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult -->

# Class ArimaResult (3.40.0)

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

## Attributes |
|
|---|---|
Name |
Description |
`arima_model_info` |
`Sequence[`
This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |

## Classes

### ArimaCoefficients

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

### ArimaModelInfo

`ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima model information.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytabletablereference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference -->

# Class TableReference (3.40.0)

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
