---
merged_at: 2026-01-26T21:00:49.250061
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineroutine.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine -->

# Class Routine (3.40.0)

`Routine(routine_ref, **kwargs)`


Resource representing a user-defined routine.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines)

## Parameters |
|
|---|---|
Name |
Description |
`routine_ref` |
`Union[str, `
A pointer to a routine. If |
|
`Dict`
Initial property values. |

## Properties

### arguments

List[[google.cloud.bigquery.routine.RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument)]: Input/output
argument of a function or a stored procedure.

In-place modification is not supported. To set, replace the entire
property value with the modified list of
[RoutineArgument](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument) objects.

### body

str: The body of the routine.

### created

Optional[datetime.datetime]: Datetime at which the routine was
created (:data:`None`

until set from the server).

Read-only.

### data_governance_type

Optional[str]: If set to `DATA_MASKING`

, the function is validated
and made available as a masking function.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not :data:`string` or :data:`None` . |

### dataset_id

str: ID of dataset containing the routine.

### description

Optional[str]: Description of the routine (defaults to
:data:`None`

).

### determinism_level

Optional[str]: (experimental) The determinism level of the JavaScript UDF if defined.

### etag

str: ETag for the resource (:data:`None`

until set from the
server).

Read-only.

### external_runtime_options

Optional[[google.cloud.bigquery.routine.ExternalRuntimeOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions)]:
Configures the external runtime options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### imported_libraries

List[str]: The path of the imported JavaScript libraries.

The [language](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) must
equal `JAVACRIPT`

.

Examples:
Set the `imported_libraries`

to a list of Google Cloud Storage
URIs.

```
.. code-block:: python
routine = bigquery.Routine("proj.dataset.routine_id")
routine.imported_libraries = [
"gs://cloud-samples-data/bigquery/udfs/max-value.js",
]
```


### language

Optional[str]: The language of the routine.

Defaults to `SQL`

.

### modified

Optional[datetime.datetime]: Datetime at which the routine was
last modified (:data:`None`

until set from the server).

Read-only.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### reference

[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference): Reference
describing the ID of this routine.

### remote_function_options

Optional[[google.cloud.bigquery.routine.RemoteFunctionOptions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RemoteFunctionOptions)]:
Configures remote function options for a routine.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the value is not
`None` . |

### return_table_type

The return type of a Table Valued Function (TVF) routine.

.. versionadded:: 2.22.0

### return_type

google.cloud.bigquery.StandardSqlDataType: Return type of the routine.

If absent, the return type is inferred from
[body](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.Routine) at query time in
each query that references this routine. If present, then the
evaluated result will be cast to the specified returned type at query
time.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Routine.FIELDS.return_type)

### routine_id

str: The routine ID.

### type_

str: The fine-grained type of the routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#RoutineType)

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.routine.routine.Routine`


Factory: construct a routine given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Resource, as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.Routine` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine represented as an API resource. |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigquery_v2typesmodeldatasplitmethod_googlecloudbigquery_v2typesmo_d49d07.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodeldatasplitmethod_googlecloudbigquery_v2typesmod_3cf5a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeldatasplitmethod_googlecloudbigquery_v2typesmode_07026b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeldatasplitmethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.DataSplitMethod -->

# Class DataSplitMethod (3.40.0)

`DataSplitMethod(value)`


Indicates the method to split input data into multiple tables.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelfeedbacktype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.FeedbackType -->

# Class FeedbackType (3.40.0)

`FeedbackType(value)`


Indicates the training algorithm to use for matrix factorization models.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumssqltypenames_googlecloudbigqueryquerysqlparameterscalar_b6b6ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumssqltypenames.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SqlTypeNames -->

# Class SqlTypeNames (3.40.0)

`SqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryquerysqlparameterscalartypes.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes -->

# Class SqlParameterScalarTypes (3.40.0)

`SqlParameterScalarTypes()`


Supported scalar SQL query parameter types as type objects.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodeloptimizationstrategy_googlecloudbigquery_v2typ_d87b88.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodeloptimizationstrategy_googlecloudbigquery_v2type_d4a977.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodeloptimizationstrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.OptimizationStrategy -->

# Class OptimizationStrategy (3.40.0)

`OptimizationStrategy(value)`


Indicates the optimization strategy used for training.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesstandardsqldatatypetypekind.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType.TypeKind -->

# Class TypeKind (3.40.0)

`TypeKind(value)`


API documentation for `bigquery_v2.types.StandardSqlDataType.TypeKind`

class.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumstimestampprecision_googlecloudbigquerydbapioperationale_b9264a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumstimestampprecision.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision -->

# Class TimestampPrecision (3.40.0)

`TimestampPrecision(value)`


Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapioperationalerror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.OperationalError -->

# Class OperationalError (3.40.0)

DB-API error related to the database operation.

These errors are not necessarily under the control of the programmer.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.UnknownJob -->

# Class UnknownJob (3.40.0)

`UnknownJob(job_id, client)`


A job whose type cannot be determined.

## Properties

### configuration

Job-type specific configurtion.

### created

Datetime at which the job was created.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the creation time (None until set from the server). |

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

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.base.UnknownJob`


Construct an UnknownJob from the JSON representation.

Parameters |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON representation of a job. |
`client` |
Client connected to BigQuery API. |

Returns |
|
|---|---|
Type |
Description |
`UnknownJob` |
Job corresponding to the resource. |

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


Generate a resource for the job.
