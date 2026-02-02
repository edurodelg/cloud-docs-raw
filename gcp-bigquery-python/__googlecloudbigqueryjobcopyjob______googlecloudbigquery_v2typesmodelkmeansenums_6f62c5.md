---
merged_at: 2026-02-02T16:19:10.383084
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJob -->

# Class CopyJob (3.40.0)

`CopyJob(job_id, sources, destination, client, job_config=None)`


Asynchronous job: copy data into a table from other tables.

## Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`str`
the job's ID, within the project belonging to |
`sources` |
`List[`
Table from which data is to be loaded. |
`destination` |
Table into which data is to be loaded. |
`client` |
A client which holds credentials and project configuration for the dataset (which requires a project). |
`job_config` |
`Optional[`
Extra configuration options for the copy job. |

## Properties

### configuration

The configuration for this copy job.

### create_disposition

See
[create_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig).

### created

Datetime at which the job was created.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the creation time (None until set from the server). |

### destination

[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference): Table into which data
is to be loaded.

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### ended

Datetime at which the job finished.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the end time (None until set from the server). |

### error_result

Output only. Final error result of the job.

If present, indicates that the job has completed and was unsuccessful.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result)

Returns |
|
|---|---|
Type |
Description |
`Optional[Mapping]` |
the error information (None until set from the server). |

### errors

Output only. The first errors encountered during the running of the job.

The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has not completed or was unsuccessful.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors)

Returns |
|
|---|---|
Type |
Description |
`Optional[List[Mapping]]` |
the error information (None until set from the server). |

### etag

ETag for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the ETag (None until set from the server). |

### job_id

str: ID of the job.

### job_type

Type of job.

Returns |
|
|---|---|
Type |
Description |
`str` |
one of 'load', 'copy', 'extract', 'query'. |

### labels

Dict[str, str]: Labels for the job.

### location

str: Location where the job runs.

### num_child_jobs

The number of child jobs executed.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs)

### parent_job_id

Return the ID of the parent job.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.parent_job_id](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.parent_job_id)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
parent job id. |

### path

URL path for the job's APIs.

Returns |
|
|---|---|
Type |
Description |
`str` |
the path based on project and job ID. |

### project

Project bound to the job.

Returns |
|
|---|---|
Type |
Description |
`str` |
the project (derived from the client). |

### reservation_id

str: Name of the primary reservation assigned to this job.

Note that this could be different than reservations reported in the reservation field if parent reservations were used to execute this job.

### reservation_usage

Job resource usage breakdown by reservation.

Returns |
|
|---|---|
Type |
Description |
`List[` |
Reservation usage stats. Can be empty if not set from the server. |

### script_statistics

Statistics for a child job of a script.

### self_link

URL for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the URL (None until set from the server). |

### session_info

[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

### sources

List[[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)]): Table(s) from
which data is to be loaded.

### started

Datetime at which the job was started.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the start time (None until set from the server). |

### state

Output only. Running state of the job.

Valid states include 'PENDING', 'RUNNING', and 'DONE'.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.state](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.state)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the state (None until set from the server). |

### transaction_info

Information of the multi-statement transaction if this job is part of one.

Since a scripting query job can execute multiple transactions, this
property is only expected on child jobs. Use the
[list_jobs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client) method with the
`parent_job`

parameter to iterate over child jobs.

.. versionadded:: 2.24.0

### user_email

E-mail address of user who submitted the job.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the URL (None until set from the server). |

### write_disposition

See
[write_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.CopyJobConfig).

## Methods

### add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

If the operation is not already complete, this will start a helper thread to poll for the status of the operation in the background.

Parameter |
|
|---|---|
Name |
Description |
`fn` |
`Callable[Future]`
The callback to execute when the operation is complete. |

### cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel)

Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Boolean indicating that the cancel request was sent. |

### cancelled

`cancelled()`


Check if the job has been cancelled.

This always returns False. It's not possible to check if a job was
cancelled in the API. This method is here to satisfy the interface
for `google.api_core.future.Future`

.

Returns |
|
|---|---|
Type |
Description |
`bool` |
False |

### done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`reload` |
`Optional[bool]`
If |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. If the job state is |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if the job is complete, False otherwise. |

### exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

See the documentation for the `result`

method for details on how
this method operates, as both `result`

and this method rely on the
exact same polling logic. The only difference is that this method does
not accept `retry`

and `polling`

arguments but relies on the default ones
instead.

Parameter |
|
|---|---|
Name |
Description |
`timeout` |
`int`
How long to wait for the operation to complete. |

Returns |
|
|---|---|
Type |
Description |
`Optional[google.api_core.GoogleAPICallError]` |
The operation's error. |

### exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Boolean indicating existence of the job. |

### from_api_repr

`from_api_repr(resource, client)`


Factory: construct a job given its API representation

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
dataset job representation returned from the API |
`client` |
Client which holds credentials and project configuration for the dataset. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.CopyJob` |
Job parsed from `resource` . |

### reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |

### result

```
result(
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.base._AsyncJob
```


Start the job and wait for it to complete and get the result.

Parameters |
|
|---|---|
Name |
Description |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. If the job state is |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.GoogleAPICallError` |
if the job failed. |
`concurrent.futures.TimeoutError` |
if the job did not complete in the given timeout. |

Returns |
|
|---|---|
Type |
Description |
`_AsyncJob` |
This instance. |

### running

`running()`


True if the operation is currently running.

### set_exception

`set_exception(exception)`


Set the Future's exception.

### set_result

`set_result(result)`


Set the Future's result.

### to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.KmeansEnums.KmeansInitializationMethod -->

# Class KmeansInitializationMethod (3.40.0)

`KmeansInitializationMethod(value)`


Indicates the method used to initialize the centroids for KMeans clustering algorithm.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.Encoding -->

# Class Encoding (3.40.0)

`Encoding()`


The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStatistics -->

# Class ScriptStatistics (3.40.0)

`ScriptStatistics(resource)`


Statistics for a child job of a script.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### evaluation_kind

str: Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

### stack_frames

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.PartitionRange -->

# Class PartitionRange (3.40.0)

`PartitionRange(start=None, end=None, interval=None, _properties=None)`


Definition of the ranges for range partitioning.

## Parameters |
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

## Properties

### end

int: The end of range partitioning, exclusive.

### interval

int: The width of each interval.

### start

int: The start of range partitioning, inclusive.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableConstraints -->

# Class TableConstraints (3.40.0)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics -->

# Class ScriptStatistics (3.40.0)

`ScriptStatistics(resource)`


Statistics for a child job of a script.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### evaluation_kind

str: Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

### stack_frames

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest -->

# Class ListModelsRequest (3.40.0)

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the models to list. |
`dataset_id` |
`str`
Required. Dataset ID of the models to list. |
`max_results` |
`google.protobuf.wrappers_pb2.UInt32Value`
The maximum number of results to return in a single response page. Leverage the page tokens to iterate through the entire collection. |
`page_token` |
`str`
Page token, returned by a previous call to request the next page of results |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter -->

# Class ScalarQueryParameter (3.40.0)

```
ScalarQueryParameter(
name: typing.Optional[str],
type_: typing.Optional[
typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType]
],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
)
```


Named / positional query parameters for scalar values.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ScalarQueryParameter`


Factory: construct parameter from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameter` |
Instance |

### positional

```
positional(
type_: typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
) -> google.cloud.bigquery.query.ScalarQueryParameter
```


Factory for positional paramater.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameter` |
Instance without name |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.DatasetReference -->

# Class DatasetReference (3.40.0)

`DatasetReference(project: str, dataset_id: str)`


DatasetReferences are pointers to datasets.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference](https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#datasetreference)

## Parameters |
|
|---|---|
Name |
Description |
`project` |
`str`
The ID of the project |
`dataset_id` |
`str`
The ID of the dataset |

## Properties

### dataset_id

str: Dataset ID.

### path

str: URL path for the dataset based on project and dataset ID.

### project

str: Project ID of the dataset.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.dataset.DatasetReference`


Factory: construct a dataset reference given its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, str]`
Dataset reference resource representation returned from the API |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.dataset.DatasetReference` |
Dataset reference parsed from `resource` . |

### from_string

```
from_string(
dataset_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.dataset.DatasetReference
```


Construct a dataset reference from dataset ID string.

Parameters |
|
|---|---|
Name |
Description |
`dataset_id` |
`str`
A dataset ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `dataset_id` is not a fully-qualified dataset ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`DatasetReference .. rubric:: Examples >>> DatasetReference.from_string('my-project-id.some_dataset') DatasetReference('my-project-id', 'some_dataset')` |
Dataset reference parsed from `dataset_id` . |

### model

`model(model_id)`


Constructs a ModelReference.

Parameter |
|
|---|---|
Name |
Description |
`model_id` |
`str`
the ID of the model. |

Returns |
|
|---|---|
Type |
Description |
|
A ModelReference for a model in this dataset. |

### routine

`routine(routine_id)`


Constructs a RoutineReference.

Parameter |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
the ID of the routine. |

Returns |
|
|---|---|
Type |
Description |
|
A RoutineReference for a routine in this dataset. |

### table

`table(table_id: str) -> google.cloud.bigquery.table.TableReference`


Constructs a TableReference.

Parameter |
|
|---|---|
Name |
Description |
`table_id` |
`str`
The ID of the table. |

Returns |
|
|---|---|
Type |
Description |
|
A table reference for a table in this dataset. |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this dataset reference

Returns |
|
|---|---|
Type |
Description |
`Dict[str, str]` |
dataset reference represented as an API resource |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType -->

# Class StandardSqlTableType (3.40.0)

```
StandardSqlTableType(
columns: typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField],
)
```


A table type.

## Properties

### columns

The columns in this table type.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.standard_sql.StandardSqlTableType
```


Construct an SQL table type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL table type.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptStackFrame -->

# Class ScriptStackFrame (3.40.0)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics -->

# Class MultiClassClassificationMetrics (3.40.0)

```
MultiClassClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Evaluation metrics for multi-class classification/classifier models.

## Attributes |
|
|---|---|
Name |
Description |
`aggregate_classification_metrics` |
Aggregate classification metrics. |
`confusion_matrix_list` |
`Sequence[`
Confusion matrix at different thresholds. |

## Classes

### ConfusionMatrix

`ConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for multi-class classification models.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame -->

# Class ScriptStackFrame (3.40.0)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### end_column

int: One-based end column.

### end_line

int: One-based end line.

### procedure_id

Optional[str]: Name of the active procedure.

Omitted if in a top-level script.

### start_column

int: One-based start column.

### start_line

int: One-based start line.

### text

str: Text of the current statement/expression.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query -->

# Module query (3.40.0)

BigQuery query processing.

## Classes

[ArrayQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter)

`ArrayQueryParameter(name, array_type, values)`


Named / positional query parameters for array values.

Parameters |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

[ArrayQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType)

`ArrayQueryParameterType(array_type, *, name=None, description=None)`


Type representation for array query parameters.

Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[ConnectionProperty](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty)

`ConnectionProperty(key: str = "", value: str = "")`


A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the property to set, for example, |
`value` |
`str`
The value of the property to set. |

[RangeQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter)

`RangeQueryParameter(range_element_type, start=None, end=None, name=None)`


Named / positional query parameters for range values.

Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of 'TIMESTAMP', 'DATE', or 'DATETIME'. |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`name` |
`Optional[str]`
Parameter name, used via |

[RangeQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType)

`RangeQueryParameterType(type_, *, name=None, description=None)`


Type representation for range query parameters.

Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Union[ScalarQueryParameterType, str]`
Type of range element, must be one of 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[ScalarQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter)

```
ScalarQueryParameter(
name: typing.Optional[str],
type_: typing.Optional[
typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType]
],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
)
```


Named / positional query parameters for scalar values.

[ScalarQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType)

`ScalarQueryParameterType(type_, *, name=None, description=None)`


Type representation for scalar query parameters.

Parameters |
|
|---|---|
Name |
Description |
`type_` |
`str`
One of 'STRING', 'INT64', 'FLOAT64', 'NUMERIC', 'BOOL', 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[SqlParameterScalarTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes)

`SqlParameterScalarTypes()`


Supported scalar SQL query parameter types as type objects.

[StructQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter)

`StructQueryParameter(name, *sub_params)`


Name / positional query parameters for struct values.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |

[StructQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType)

`StructQueryParameterType(*fields, name=None, description=None)`


Type representation for struct query parameters.

Parameters |
|
|---|---|
Name |
Description |
`fields` |
`Iterable[Union[ ArrayQueryParameterType, ScalarQueryParameterType, StructQueryParameterType ]]`
An non-empty iterable describing the struct's field types. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[UDFResource](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource)

`UDFResource(udf_type, value)`


Describe a single user-defined function (UDF) resource.

Parameters |
|
|---|---|
Name |
Description |
`udf_type` |
`str`
The type of the resource ('inlineCode' or 'resourceUri') |
`value` |
`str See: https://cloud.google.com/bigquery/user-defined-functions#api`
The inline code or resource URI. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Encoding -->

# Class Encoding (3.40.0)

`Encoding()`


The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage -->

# Class ReservationUsage (3.40.0)

`ReservationUsage(name, slot_ms)`


Job resource usage for a reservation.

## Methods

### ReservationUsage

`ReservationUsage(name, slot_ms)`


Create new instance of ReservationUsage(name, slot_ms)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/magics -->

# IPython Magics for BigQuery

To use these magics, you must first register them. Run the `%load_ext`

magic
in a Jupyter notebook cell.

```
%load_ext bigquery_magics
```


This makes the `%%bigquery`

magic available.

## Code Samples

Running a query:

```
%%bigquery
SELECT name, SUM(number) as count
FROM `bigquery-public-data.usa_names.usa_1910_current`
GROUP BY name
ORDER BY count DESC
LIMIT 3
```


Running a parameterized query:

```
%%bigquery --params {"corpus_name": "hamlet", "limit": 10}
SELECT word, SUM(word_count) as count
FROM `bigquery-public-data.samples.shakespeare`
WHERE corpus = @corpus_name
GROUP BY word
ORDER BY count DESC
LIMIT @limit
```

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.PolicyTagList -->

# Class PolicyTagList (3.40.0)

`PolicyTagList(names: typing.Iterable[str] = ())`


Define Policy Tags for a column.

## Properties

### names

Tuple[str]: Policy tags associated with this definition.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.PolicyTagList`


Return a `PolicyTagList`

object deserialized from a dict.

This method creates a new `PolicyTagList`

instance that points to
the `api_repr`

parameter as its internal properties dict. This means
that when a `PolicyTagList`

instance is stored as a property of
another object, any changes made at the higher level will also appear
here.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Mapping[str, str]`
The serialized representation of the PolicyTagList, such as what is output by |

Returns |
|
|---|---|
Type |
Description |
`Optional[google.cloud.bigquery.schema.PolicyTagList]` |
The `PolicyTagList` object or None. |

### to_api_repr

`to_api_repr() -> dict`


Return a dictionary representing this object.

This method returns the properties dict of the `PolicyTagList`

instance rather than making a copy. This means that when a
`PolicyTagList`

instance is stored as a property of another
object, any changes made at the higher level will also appear here.

Returns |
|
|---|---|
Type |
Description |
`dict` |
A dictionary representing the PolicyTagList object in serialized form. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType -->

# Class ScalarQueryParameterType (3.40.0)

`ScalarQueryParameterType(type_, *, name=None, description=None)`


Type representation for scalar query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`str`
One of 'STRING', 'INT64', 'FLOAT64', 'NUMERIC', 'BOOL', 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameterType` |
Instance |

### to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

### with_name

`with_name(new_name: typing.Optional[str])`


Return a copy of the instance with `name`

set to `new_name`

.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Union[str, None]`
The new name of the query parameter type. If |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameterType` |
A new instance with updated name. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType -->

# Class RangeQueryParameterType (3.40.0)

`RangeQueryParameterType(type_, *, name=None, description=None)`


Type representation for range query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Union[ScalarQueryParameterType, str]`
Type of range element, must be one of 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameterType` |
Instance |

### to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

### with_name

`with_name(new_name: typing.Optional[str])`


Return a copy of the instance with `name`

set to `new_name`

.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Union[str, None]`
The new name of the range query parameter type. If |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameterType` |
A new instance with updated name. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJob -->

# Class ExtractJob (3.40.0)

`ExtractJob(job_id, source, destination_uris, client, job_config=None)`


Asynchronous job: extract data from a table into Cloud Storage.

## Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`str`
the job's ID. |
`source` |
`Union[ `
Table or Model from which data is to be loaded or extracted. |
`destination_uris` |
`List[str]`
URIs describing where the extracted data will be written in Cloud Storage, using the format |
`client` |
A client which holds credentials and project configuration. |
`job_config` |
`Optional[`
Extra configuration options for the extract job. |

## Properties

### compression

See
[compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig).

### configuration

The configuration for this extract job.

### created

Datetime at which the job was created.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the creation time (None until set from the server). |

### destination_format

See
[destination_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig).

### destination_uri_file_counts

Return file counts from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`List[int]` |
A list of integer counts, each representing the number of files per destination URI or URI pattern specified in the extract configuration. These values will be in the same order as the URIs specified in the 'destinationUris' field. Returns None if job is not yet complete. |

### destination_uris

List[str]: URIs describing where the extracted data will be
written in Cloud Storage, using the format
`gs://<bucket_name>/<object_name_or_glob>`

.

### ended

Datetime at which the job finished.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the end time (None until set from the server). |

### error_result

Output only. Final error result of the job.

If present, indicates that the job has completed and was unsuccessful.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.error_result)

Returns |
|
|---|---|
Type |
Description |
`Optional[Mapping]` |
the error information (None until set from the server). |

### errors

Output only. The first errors encountered during the running of the job.

The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has not completed or was unsuccessful.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.errors)

Returns |
|
|---|---|
Type |
Description |
`Optional[List[Mapping]]` |
the error information (None until set from the server). |

### etag

ETag for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the ETag (None until set from the server). |

### field_delimiter

See
[field_delimiter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig).

### job_id

str: ID of the job.

### job_type

Type of job.

Returns |
|
|---|---|
Type |
Description |
`str` |
one of 'load', 'copy', 'extract', 'query'. |

### labels

Dict[str, str]: Labels for the job.

### location

str: Location where the job runs.

### num_child_jobs

The number of child jobs executed.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs)

### parent_job_id

Return the ID of the parent job.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.parent_job_id](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.parent_job_id)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
parent job id. |

### path

URL path for the job's APIs.

Returns |
|
|---|---|
Type |
Description |
`str` |
the path based on project and job ID. |

### print_header

See
[print_header](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ExtractJobConfig).

### project

Project bound to the job.

Returns |
|
|---|---|
Type |
Description |
`str` |
the project (derived from the client). |

### reservation_id

str: Name of the primary reservation assigned to this job.

Note that this could be different than reservations reported in the reservation field if parent reservations were used to execute this job.

### reservation_usage

Job resource usage breakdown by reservation.

Returns |
|
|---|---|
Type |
Description |
`List[` |
Reservation usage stats. Can be empty if not set from the server. |

### script_statistics

Statistics for a child job of a script.

### self_link

URL for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the URL (None until set from the server). |

### session_info

[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

### source

Union[ [google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference), [google.cloud.bigquery.model.ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.ModelReference) ]: Table or Model from which data is to be loaded or extracted.

### started

Datetime at which the job was started.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the start time (None until set from the server). |

### state

Output only. Running state of the job.

Valid states include 'PENDING', 'RUNNING', and 'DONE'.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.state](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatus.FIELDS.state)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the state (None until set from the server). |

### transaction_info

Information of the multi-statement transaction if this job is part of one.

Since a scripting query job can execute multiple transactions, this
property is only expected on child jobs. Use the
[list_jobs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client) method with the
`parent_job`

parameter to iterate over child jobs.

.. versionadded:: 2.24.0

### user_email

E-mail address of user who submitted the job.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the URL (None until set from the server). |

## Methods

### add_done_callback

`add_done_callback(fn)`


Add a callback to be executed when the operation is complete.

If the operation is not already complete, this will start a helper thread to poll for the status of the operation in the background.

Parameter |
|
|---|---|
Name |
Description |
`fn` |
`Callable[Future]`
The callback to execute when the operation is complete. |

### cancel

```
cancel(
client=None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: cancel job via a POST request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/cancel)

Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Boolean indicating that the cancel request was sent. |

### cancelled

`cancelled()`


Check if the job has been cancelled.

This always returns False. It's not possible to check if a job was
cancelled in the API. This method is here to satisfy the interface
for `google.api_core.future.Future`

.

Returns |
|
|---|---|
Type |
Description |
`bool` |
False |

### done

```
done(
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
reload: bool = True,
) -> bool
```


Checks if the job is complete.

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`reload` |
`Optional[bool]`
If |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. If the job state is |

Returns |
|
|---|---|
Type |
Description |
`bool` |
True if the job is complete, False otherwise. |

### exception

`exception(timeout=object)`


Get the exception from the operation, blocking if necessary.

See the documentation for the `result`

method for details on how
this method operates, as both `result`

and this method rely on the
exact same polling logic. The only difference is that this method does
not accept `retry`

and `polling`

arguments but relies on the default ones
instead.

Parameter |
|
|---|---|
Name |
Description |
`timeout` |
`int`
How long to wait for the operation to complete. |

Returns |
|
|---|---|
Type |
Description |
`Optional[google.api_core.GoogleAPICallError]` |
The operation's error. |

### exists

```
exists(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> bool
```


API call: test for the existence of the job via a GET request

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Boolean indicating existence of the job. |

### from_api_repr

```
from_api_repr(
resource: dict, client
) -> google.cloud.bigquery.job.extract.ExtractJob
```


Factory: construct a job given its API representation

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
dataset job representation returned from the API |
`client` |
Client which holds credentials and project configuration for the dataset. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.job.ExtractJob` |
Job parsed from `resource` . |

### reload

```
reload(
client=None,
retry: google.api_core.retry.retry_unary.Retry = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = 128,
)
```


API call: refresh job properties via a GET request.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/get)

Parameters |
|
|---|---|
Name |
Description |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |
`client` |
`Optional[`
the client to use. If not passed, falls back to the |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. |

### result

```
result(
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[float] = None,
) -> google.cloud.bigquery.job.base._AsyncJob
```


Start the job and wait for it to complete and get the result.

Parameters |
|
|---|---|
Name |
Description |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the RPC. If the job state is |
`timeout` |
`Optional[float]`
The number of seconds to wait for the underlying HTTP transport before using |

Exceptions |
|
|---|---|
Type |
Description |
`google.cloud.exceptions.GoogleAPICallError` |
if the job failed. |
`concurrent.futures.TimeoutError` |
if the job did not complete in the given timeout. |

Returns |
|
|---|---|
Type |
Description |
`_AsyncJob` |
This instance. |

### running

`running()`


True if the operation is currently running.

### set_exception

`set_exception(exception)`


Set the Future's exception.

### set_result

`set_result(result)`


Set the Future's result.

### to_api_repr

`to_api_repr()`


Generate a resource for `_begin`

.
