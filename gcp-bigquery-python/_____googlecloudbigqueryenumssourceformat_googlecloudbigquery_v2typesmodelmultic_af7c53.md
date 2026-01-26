---
merged_at: 2026-01-26T21:00:49.244073
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat -->

# Class SourceFormat (3.40.0)

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Row -->

# Class Row (3.40.0)

`Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single row in the confusion matrix.

## Attributes |
|
|---|---|
Name |
Description |
`actual_label` |
`str`
The original label of this row. |
`entries` |
`Sequence[`
Info describing predicted label distribution. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition -->

# Class WriteDisposition (3.40.0)

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition -->

# Class WriteDisposition (3.40.0)

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.HivePartitioningOptions -->

# Class HivePartitioningOptions (3.40.0)

`HivePartitioningOptions()`


Options that configure hive partitioning.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions)

## Properties

### mode

Optional[str]: When set, what mode of hive partitioning to use when reading data.

Two modes are supported: "AUTO" and "STRINGS".

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode)

### require_partition_filter

Optional[bool]: If set to true, queries over the partitioned table require a partition filter that can be used for partition elimination to be specified.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#HivePartitioningOptions.FIELDS.mode)

### source_uri_prefix

Optional[str]: When hive partition detection is requested, a common prefix for all source URIs is required.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.HivePartitioningOptions
```


Factory: construct a `.external_config.HivePartitioningOptions`

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
`HivePartitioningOptions` |
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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableListItem -->

# Class TableListItem (3.40.0)

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job -->

# Package job (3.40.0)

API documentation for `bigquery.job`

package.

## Classes

[Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Compression)

The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

[CopyJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob)

Asynchronous job: copy data into a table from other tables.

[CopyJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig)

Configuration options for copy jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CreateDisposition)

Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

[DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat)

The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

[DmlStats](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DmlStats)

Detailed statistics for DML statements.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats](https://cloud.google.com/bigquery/docs/reference/rest/v2/DmlStats)

[Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding)

The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

[ExtractJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob)

Asynchronous job: extract data from a table into Cloud Storage.

[ExtractJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig)

Configuration options for extract jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[IncrementalResultStats](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.IncrementalResultStats)

IncrementalResultStats provides information about incremental query execution.

[LoadJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob)

Asynchronous job for loading data into a table.

Can load from Google Cloud Storage URIs or from a file.

[LoadJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig)

Configuration options for load jobs.

Set properties on the constructed configuration by using the property name
as the name of a keyword argument. Values which are unset or :data:`None`

use the BigQuery REST API default values. See the ```
BigQuery REST API
reference documentation
<https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad>
```

_
for a list of default values.

Required options differ based on the
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) value.
For example, the BigQuery API's default value for
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) is `"CSV"`

.
When loading a CSV file, either
[schema](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) must be set or
[autodetect](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig) must be set to
:data:`True`

.

[OperationType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.OperationType)

Different operation types supported in table copy job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#operationtype)

[QueryJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob)

Asynchronous job: query tables.

[QueryJobConfig](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig)

Configuration options for query jobs.

All properties in this class are optional. Values which are :data:`None`

->
server defaults. Set properties on the constructed configuration by using
the property name as the name of a keyword argument.

[QueryPlanEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntry)

QueryPlanEntry represents a single stage of a query execution plan.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ExplainQueryStage)
for the underlying API representation within query statistics.

[QueryPlanEntryStep](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPlanEntryStep)

Map a single step in a query plan entry.

[QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryPriority)

Specifies a priority for the query. The default value is
`INTERACTIVE`

.

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ReservationUsage)

Job resource usage for a reservation.

[SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption)

Specifies an update to the destination table schema as a side effect of a load job.

[ScriptOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions)

Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions)

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame)

Stack frame showing the line/column/procedure name where the current evaluation happened.

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics)

Statistics for a child job of a script.

[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)

The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

[TimelineEntry](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry)

TimelineEntry represents progress of a query job at a particular point in time.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample)
for the underlying API representation within query statistics.

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TransactionInfo)

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob)

A job whose type cannot be determined.

[WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.WriteDisposition)

Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.
