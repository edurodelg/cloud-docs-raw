---
merged_at: 2026-01-26T23:27:21.523413
merged_files: 2
---


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
