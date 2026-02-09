---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob
fetched_at: 2026-02-09T09:40:58.880702
---

# Class QueryJob (3.40.0)

`QueryJob(job_id, query, client, job_config=None)`


Asynchronous job: query tables.

## Parameters |
|
|---|---|
Name |
Description |
`job_id` |
`str`
the job's ID, within the project belonging to |
`query` |
`str`
SQL query string. |
`client` |
A client which holds credentials and project configuration for the dataset (which requires a project). |
`job_config` |
`Optional[`
Extra configuration options for the query job. |

## Properties

### allow_large_results

See
[allow_large_results](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### billing_tier

Return billing tier from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.billing_tier](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.billing_tier)

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
Billing tier used by the job, or None if job is not yet complete. |

### cache_hit

Return whether or not query results were served from cache.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.cache_hit](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.cache_hit)

Returns |
|
|---|---|
Type |
Description |
`Optional[bool]` |
whether the query results were returned from cache, or None if job is not yet complete. |

### clustering_fields

See
[clustering_fields](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### configuration

The configuration for this query job.

### connection_properties

.. versionadded:: 2.29.0

### create_disposition

See
[create_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### create_session

See
[create_session](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

.. versionadded:: 2.29.0

### created

Datetime at which the job was created.

Returns |
|
|---|---|
Type |
Description |
`Optional[datetime.datetime]` |
the creation time (None until set from the server). |

### ddl_operation_performed

Optional[str]: Return the DDL operation performed.

### ddl_target_routine

Optional[[google.cloud.bigquery.routine.RoutineReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference)]: Return the DDL target routine, present
for CREATE/DROP FUNCTION/PROCEDURE queries.

### ddl_target_table

Optional[[google.cloud.bigquery.table.TableReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.TableReference)]: Return the DDL target table, present
for CREATE/DROP TABLE/VIEW queries.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.ddl_target_table](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.ddl_target_table)

### default_dataset

See
[default_dataset](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### destination

See
[destination](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### destination_encryption_configuration

[google.cloud.bigquery.encryption_configuration.EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration): Custom
encryption configuration for the destination table.

Custom encryption configuration (e.g., Cloud KMS keys) or :data:`None`

if using default encryption.

### dry_run

See
[dry_run](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

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

### estimated_bytes_processed

Return the estimated number of bytes processed by the query.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
number of DML rows affected by the job, or None if job is not yet complete. |

### etag

ETag for the job resource.

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
the ETag (None until set from the server). |

### flatten_results

See
[flatten_results](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

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

### maximum_billing_tier

See
[maximum_billing_tier](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### maximum_bytes_billed

See
[maximum_bytes_billed](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### num_child_jobs

The number of child jobs executed.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics.FIELDS.num_child_jobs)

### num_dml_affected_rows

Return the number of DML rows affected by the job.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
number of DML rows affected by the job, or None if job is not yet complete. |

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

### priority

See
[priority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### project

Project bound to the job.

Returns |
|
|---|---|
Type |
Description |
`str` |
the project (derived from the client). |

### query

str: The query text used in this query job.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.query](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobConfigurationQuery.FIELDS.query)

### query_id

[Preview] ID of a completed query.

This ID is auto-generated and not guaranteed to be populated.

### query_parameters

See
[query_parameters](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### query_plan

Return query plan from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.query_plan](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.query_plan)

Returns |
|
|---|---|
Type |
Description |
`List[` |
mappings describing the query plan, or an empty list if the query has not yet completed. |

### range_partitioning

See
[range_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### referenced_tables

Return referenced tables from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.referenced_tables](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.referenced_tables)

Returns |
|
|---|---|
Type |
Description |
`List[Dict]` |
mappings describing the query plan, or an empty list if the query has not yet completed. |

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

The schema of the results.

Present only for successful dry run of non-legacy SQL queries.

### schema_update_options

### script_statistics

Statistics for a child job of a script.

### search_stats

Returns a SearchStats object.

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

### slot_millis

Union[int, None]: Slot-milliseconds used by this query job.

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

### statement_type

Return statement type from job statistics, if present.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.statement_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#JobStatistics2.FIELDS.statement_type)

Returns |
|
|---|---|
Type |
Description |
`Optional[str]` |
type of statement used by the job, or None if job is not yet complete. |

### table_definitions

See
[table_definitions](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### time_partitioning

See
[time_partitioning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### timeline

List(TimelineEntry): Return the query execution timeline from job statistics.

### total_bytes_billed

Return total bytes billed from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
Total bytes processed by the job, or None if job is not yet complete. |

### total_bytes_processed

Return total bytes processed from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`Optional[int]` |
Total bytes processed by the job, or None if job is not yet complete. |

### transaction_info

Information of the multi-statement transaction if this job is part of one.

Since a scripting query job can execute multiple transactions, this
property is only expected on child jobs. Use the
[list_jobs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client) method with the
`parent_job`

parameter to iterate over child jobs.

.. versionadded:: 2.24.0

### udf_resources

See
[udf_resources](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### undeclared_query_parameters

Return undeclared query parameters from job statistics, if present.

Returns |
|
|---|---|
Type |
Description |
`List[Union[ ` |
Undeclared parameters, or an empty list if the query has not yet completed. |

### use_legacy_sql

See
[use_legacy_sql](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

### use_query_cache

See
[use_query_cache](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

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
[write_disposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig).

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

`from_api_repr(resource: dict, client: Client) -> QueryJob`


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
`google.cloud.bigquery.job.QueryJob` |
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
page_size: typing.Optional[int] = None,
max_results: typing.Optional[int] = None,
retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
timeout: typing.Optional[typing.Union[float, object]] = object,
start_index: typing.Optional[int] = None,
job_retry: typing.Optional[
google.api_core.retry.retry_unary.Retry
] = google.api_core.retry.retry_unary.Retry,
) -> typing.Union[RowIterator, google.cloud.bigquery.table._EmptyRowIterator]
```


Start the job and wait for it to complete and get the result.

Parameters |
|
|---|---|
Name |
Description |
`page_size` |
`Optional[int]`
The maximum number of rows in each page of results from this request. Non-positive values are ignored. |
`max_results` |
`Optional[int]`
The maximum total number of rows from this request. |
`retry` |
`Optional[google.api_core.retry.Retry]`
How to retry the call that retrieves rows. This only applies to making RPC calls. It isn't used to retry failed jobs. This has a reasonable default that should only be overridden with care. If the job state is |
`timeout` |
`Optional[Union[float, google.api_core.future.polling.PollingFuture._DEFAULT_VALUE, ]]`
The number of seconds to wait for the underlying HTTP transport before using |
`start_index` |
`Optional[int]`
The zero-based index of the starting row to read. |
`job_retry` |
`Optional[google.api_core.retry.Retry]`
How to retry failed jobs. The default retries rate-limit-exceeded errors. Passing |

Exceptions |
|
|---|---|
Type |
Description |
`google.api_core.exceptions.GoogleAPICallError` |
If the job failed and retries aren't successful. |
`concurrent.futures.TimeoutError` |
If the job did not complete in the given timeout. |
`TypeError` |
If Non-`None` and non-default `job_retry` is provided and the job is not retryable. |

Returns |
|
|---|---|
Type |
Description |
|
Iterator of row data
`total_rows` attribute set, which counts the total number of rows **in the result set** (this is distinct from the total number of rows in the current page: `iterator.page.num_items` ). If the query is a special query that produces no results, e.g. a DDL query, an `_EmptyRowIterator` instance is returned. |

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

### to_arrow

```
to_arrow(
progress_bar_type: typing.Optional[str] = None,
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
) -> pyarrow.Table
```


[Beta] Create a class:`pyarrow.Table`

by loading all pages of a
table or query.

Parameters |
|
|---|---|
Name |
Description |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This API is a billable API. This method requires |
`create_bqstorage_client` |
`Optional[bool]`
If |
`max_results` |
`Optional[int]`
Maximum number of rows to include in the result. No limit by default. .. versionadded:: 2.21.0 |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `pyarrow` library cannot be imported. .. versionadded:: 1.17.0 |

### to_dataframe

```
to_dataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
geography_as_object: bool = False,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
date_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.DATE_DTYPE,
datetime_dtype: typing.Optional[typing.Any] = None,
time_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.TIME_DTYPE,
timestamp_dtype: typing.Optional[typing.Any] = None,
range_date_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATE_DTYPE,
range_datetime_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_DATETIME_DTYPE,
range_timestamp_dtype: typing.Optional[
typing.Any
] = DefaultPandasDTypes.RANGE_TIMESTAMP_DTYPE,
) -> pandas.DataFrame
```


Return a pandas DataFrame from a QueryJob

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This API is a billable API. This method requires the |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`create_bqstorage_client` |
`Optional[bool]`
If |
`max_results` |
`Optional[int]`
Maximum number of rows to include in the result. No limit by default. .. versionadded:: 2.21.0 |
`geography_as_object` |
`Optional[bool]`
If |
`bool_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`int_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`float_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`string_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`date_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`datetime_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`time_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`timestamp_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`range_date_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype, such as: .. code-block:: python pandas.ArrowDtype(pyarrow.struct( [("start", pyarrow.date32()), ("end", pyarrow.date32())] )) to convert BigQuery RANGE
|
`range_datetime_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype, such as: .. code-block:: python pandas.ArrowDtype(pyarrow.struct( [ ("start", pyarrow.timestamp("us")), ("end", pyarrow.timestamp("us")), ] )) to convert BigQuery RANGE
|
`range_timestamp_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype, such as: .. code-block:: python pandas.ArrowDtype(pyarrow.struct( [ ("start", pyarrow.timestamp("us", tz="UTC")), ("end", pyarrow.timestamp("us", tz="UTC")), ] )) to convert BigQuery RANGE
|

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `pandas` library cannot be imported, or the bigquery_storage_v1 module is required but cannot be imported. Also if `geography_as_object` is `True` , but the `shapely` library cannot be imported. |

Returns |
|
|---|---|
Type |
Description |
`pandas.DataFrame` |
A `pandas.DataFrame` populated with row data and column headers from the query results. The column headers are derived from the destination table's schema. |

### to_geodataframe

```
to_geodataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
max_results: typing.Optional[int] = None,
geography_column: typing.Optional[str] = None,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
) -> geopandas.GeoDataFrame
```


Return a GeoPandas GeoDataFrame from a QueryJob

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This API is a billable API. This method requires the |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`create_bqstorage_client` |
`Optional[bool]`
If |
`max_results` |
`Optional[int]`
Maximum number of rows to include in the result. No limit by default. .. versionadded:: 2.21.0 |
`geography_column` |
`Optional[str]`
If there are more than one GEOGRAPHY column, identifies which one to use to construct a GeoPandas GeoDataFrame. This option can be ommitted if there's only one GEOGRAPHY column. |
`bool_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`int_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`float_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |
`string_dtype` |
`Optional[pandas.Series.dtype, None]`
If set, indicate a pandas ExtensionDtype (e.g. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `geopandas` library cannot be imported, or the bigquery_storage_v1 module is required but cannot be imported. .. versionadded:: 2.24.0 |

Returns |
|
|---|---|
Type |
Description |
`geopandas.GeoDataFrame` |
A `geopandas.GeoDataFrame` populated with row data and column headers from the query results. The column headers are derived from the destination table's schema. |