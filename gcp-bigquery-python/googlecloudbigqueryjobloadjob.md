---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJob
fetched_at: 2026-01-25T15:32:49.177934
---

# Class LoadJob (3.40.0)

`LoadJob(job_id, source_uris, destination, client, job_config=None)`


Asynchronous job for loading data into a table.

Can load from Google Cloud Storage URIs or from a file.

## Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`str`
the job's ID |
`source_uris` |
`Optional[Sequence[str]]`
URIs of one or more data files to be loaded. See |
`destination` |
reference to table into which data is to be loaded. |
`client` |
A client which holds credentials and project configuration for the dataset (which requires a project). |

## Properties

### allow_jagged_rows

See
[allow_jagged_rows](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### allow_quoted_newlines

### autodetect

See
[autodetect](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### clustering_fields

See
[clustering_fields](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### configuration

The configuration for this load job.

### connection_properties

.. versionadded:: 3.7.0

### create_disposition

See
[create_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### create_session

See
[create_session](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

.. versionadded:: 3.7.0

### created

Datetime at which the job was created.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the creation time (None until set from the server). |

### date_format

See
[date_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### datetime_format

See
[datetime_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### destination

[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference): table where loaded rows are written

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys)
or :data:`None`

if using default encryption.

### destination_table_description

Optional[str] name given to destination table.

### destination_table_friendly_name

Optional[str] name given to destination table.

### encoding

See
[encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

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
[field_delimiter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### ignore_unknown_values

### input_file_bytes

Count of bytes loaded from source files.

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
for invalid value types. |

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
the count (None until set from the server). |

### input_files

Count of source files.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
the count (None until set from the server). |

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

### max_bad_records

See
[max_bad_records](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### null_marker

See
[null_marker](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### null_markers

See
[null_markers](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### num_child_jobs

The number of child jobs executed.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs)

### output_bytes

Count of bytes saved to destination table.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
the count (None until set from the server). |

### output_rows

Count of rows saved to destination table.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
the count (None until set from the server). |

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

### quote_character

See
[quote_character](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### range_partitioning

See
[range_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### reference_file_schema_uri

See:
attr:`<xref uid="google.cloud.bigquery.job.LoadJobConfig.reference_file_schema_uri">google.cloud.bigquery.job.LoadJobConfig.reference_file_schema_uri</xref>`

.

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

### schema

See
[schema](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### schema_update_options

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

### skip_leading_rows

See
[skip_leading_rows](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### source_column_match

See
[source_column_match](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### source_format

See
[source_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### source_uris

Optional[Sequence[str]]: URIs of data files to be loaded. See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.source_uris](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.source_uris)
for supported URI formats. None for jobs that load from a file.

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

### time_format

See
[time_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### time_partitioning

See
[time_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### time_zone

See
[time_zone](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### timestamp_format

See
[timestamp_format](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

### transaction_info

Information of the multi-statement transaction if this job is part of one.

Since a scripting query job can execute multiple transactions, this
property is only expected on child jobs. Use the
[list_jobs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client) method with the
`parent_job`

parameter to iterate over child jobs.

.. versionadded:: 2.24.0

### use_avro_logical_types

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
[write_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig).

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

`from_api_repr(resource: dict, client) -> google.cloud.bigquery.job.load.LoadJob`


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
`google.cloud.bigquery.job.LoadJob` |
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