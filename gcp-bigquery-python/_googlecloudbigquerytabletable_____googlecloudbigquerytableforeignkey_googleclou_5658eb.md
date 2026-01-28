---
merged_at: 2026-01-28T07:38:10.301760
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Table -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.ForeignKey -->

# Class ForeignKey (3.40.0)

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ClusterInfo -->

# Class ClusterInfo (3.40.0)

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

## Attributes |
|
|---|---|
Name |
Description |
`centroid_id` |
`int`
Centroid id. |
`cluster_radius` |
`google.protobuf.wrappers_pb2.DoubleValue`
Cluster radius, the average distance from centroid to each point assigned to the cluster. |
`cluster_size` |
`google.protobuf.wrappers_pb2.Int64Value`
Cluster size, the total number of points assigned to the cluster. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun -->

# Class TrainingRun (3.40.0)

`TrainingRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single training query run for the model.

## Attributes |
|
|---|---|
Name |
Description |
`training_options` |
Options that were used for this training run, includes user specified and default options that were used. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The start time of this training run. |
`results` |
`Sequence[`
Output of each iteration run, results.size() <= max_iterations.=""> |
`evaluation_metrics` |
The evaluation metrics over training/eval data that were computed at the end of training. |
`data_split_result` |
Data split result of the training run. Only set when the input data is actually split. |
`global_explanations` |
`Sequence[`
Global explanations for important features of the model. For multi-class models, there is one entry for each label class. For other models, there is only one entry in the list. |

## Classes

### IterationResult

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

### TrainingOptions

`TrainingOptions(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options used in model training.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client -->

# Module client (3.40.0)

Client for interacting with the Google BigQuery API.

## Classes

[Client](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client)

```
Client(
project: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
_http: typing.Optional[requests.sessions.Session] = None,
location: typing.Optional[str] = None,
default_query_job_config: typing.Optional[
google.cloud.bigquery.job.query.QueryJobConfig
] = None,
default_load_job_config: typing.Optional[
google.cloud.bigquery.job.load.LoadJobConfig
] = None,
client_info: typing.Optional[google.api_core.client_info.ClientInfo] = None,
client_options: typing.Optional[
typing.Union[
google.api_core.client_options.ClientOptions, typing.Dict[str, typing.Any]
]
] = None,
default_job_creation_mode: typing.Optional[str] = None,
)
```


Client to bundle configuration needed for API requests.

Parameters |
|
|---|---|
Name |
Description |
`project` |
`Optional[str]`
Project ID for the project which the client acts on behalf of. Will be passed when creating a dataset / job. If not passed, falls back to the default inferred from the environment. |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The OAuth2 Credentials to use for this client. If not passed (and if no |
`_http` |
`Optional[requests.Session]`
HTTP object to make requests. Can be any object that defines |
`location` |
`Optional[str]`
Default location for jobs / datasets / tables. |
`default_query_job_config` |
`Optional[`
Default |
`default_load_job_config` |
`Optional[`
Default |
`client_info` |
`Optional[google.api_core.client_info.ClientInfo]`
The client info used to send a user-agent string along with API requests. If |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, Dict]]`
Client options used to set user options on the client. API Endpoint should be set through client_options. |
`default_job_creation_mode` |
`Optional[str]`
Sets the default job creation mode used by query methods such as query_and_wait(). For lightweight queries, JOB_CREATION_OPTIONAL is generally recommended. |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.DefaultCredentialsError` |
Raised if `credentials` is not specified and the library fails to acquire default credentials. |

[Project](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Project)

`Project(project_id, numeric_id, friendly_name)`


Wrapper for resource describing a BigQuery project.

Parameters |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Opaque ID of the project |
`numeric_id` |
`int`
Numeric ID of the project |
`friendly_name` |
`str`
Display name of the project |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.format_options.ParquetOptions -->

# Class ParquetOptions (3.40.0)

`ParquetOptions()`


Additional options if the PARQUET source format is used.

## Properties

### enable_list_inference

Indicates whether to use schema inference specifically for Parquet LIST logical type.

### enum_as_string

Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#ParquetOptions.FIELDS.enum_as_string)

### map_target_type

Indicates whether to simplify the representation of parquet maps to only show keys and values.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, bool],
) -> google.cloud.bigquery.format_options.ParquetOptions
```


Factory: construct an instance from a resource dict.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, bool]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
|
Configuration parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Build an API representation of this object.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, bool]` |
A dictionary in the format used by the BigQuery API. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField -->

# Class StandardSqlField (3.40.0)

```
StandardSqlField(
name: typing.Optional[str] = None,
type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
)
```


A field or a column.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField)

## Parameters |
|
|---|---|
Name |
Description |
`name` |
`typing.Optional[str]`
The name of this field. Can be absent for struct fields. |
`type` |
`typing.Optional[`
The type of this parameter. Absent if not explicitly specified. For example, CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |

## Properties

### name

The name of this field. Can be absent for struct fields.

### type

The type of this parameter. Absent if not explicitly specified.

For example, CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field).

## Methods

### from_api_repr

`from_api_repr(resource: typing.Dict[str, typing.Any])`


Construct an SQL field instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL field.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions -->

# Class ScriptOptions (3.40.0)

```
ScriptOptions(
statement_timeout_ms: typing.Optional[int] = None,
statement_byte_budget: typing.Optional[int] = None,
key_result_statement: typing.Optional[
google.cloud.bigquery.enums.KeyResultStatementKind
] = None,
)
```


Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions)

## Properties

### key_result_statement

Determines which statement in the script represents the "key result".

This is used to populate the schema and query results of the script job.
Default is `KeyResultStatementKind.LAST`

.

### statement_byte_budget

Limit on the number of bytes billed per statement.

Exceeding this budget results in an error.

### statement_timeout_ms

Timeout period for each statement in a script.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.job.query.ScriptOptions
```


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.ScriptOptions` |
ScriptOptions sample parsed from `resource` . |

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics.BinaryConfusionMatrix -->

# Class BinaryConfusionMatrix (3.40.0)

`BinaryConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for binary classification models.

## Attributes |
|
|---|---|
Name |
Description |
`positive_class_threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Threshold value used when computing each of the following metric. |
`true_positives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of true samples predicted as true. |
`false_positives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of false samples predicted as true. |
`true_negatives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of true samples predicted as false. |
`false_negatives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of false samples predicted as false. |
`precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
The fraction of actual positive predictions that had positive actual labels. |
`recall` |
`google.protobuf.wrappers_pb2.DoubleValue`
The fraction of actual positive labels that were given a positive prediction. |
`f1_score` |
`google.protobuf.wrappers_pb2.DoubleValue`
The equally weighted average of recall and precision. |
`accuracy` |
`google.protobuf.wrappers_pb2.DoubleValue`
The fraction of predictions given the correct label. |
