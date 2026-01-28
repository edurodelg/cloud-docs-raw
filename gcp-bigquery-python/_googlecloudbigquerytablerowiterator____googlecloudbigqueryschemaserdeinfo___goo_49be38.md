---
merged_at: 2026-01-28T07:38:10.304254
merged_files: 2
---


---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.RowIterator -->

# Class RowIterator (3.40.0)

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

## Parameters |
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

## Properties

### created

If representing query results, the creation time of the associated query.

### ended

If representing query results, the end time of the associated query.

### job_id

ID of the query job (if applicable).

To get the job metadata, call
`job = client.get_job(rows.job_id, location=rows.location)`

.

### location

Location where the query executed (if applicable).

### num_dml_affected_rows

If this RowIterator is the result of a DML query, the number of rows that were affected.

### project

GCP Project ID where these rows are read from.

### query

The query text used.

### query_id

[Preview] ID of a completed query.

This ID is auto-generated and not guaranteed to be populated.

### schema

List[[google.cloud.bigquery.schema.SchemaField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SchemaField)]: The subset of
columns to be read from the table.

### slot_millis

Number of slot ms the user is actually billed for.

### started

If representing query results, the start time of the associated query.

### total_bytes_processed

total bytes processed from job statistics, if present.

### total_rows

int: The total number of rows in the table or query results.

## Methods

### to_arrow

```
to_arrow(
progress_bar_type: typing.Optional[str] = None,
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
create_bqstorage_client: bool = True,
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

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `pyarrow` library cannot be imported. .. versionadded:: 1.17.0 |

### to_arrow_iterable

```
to_arrow_iterable(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
max_queue_size: int = object,
max_stream_count: typing.Optional[int] = None,
) -> typing.Iterator[pyarrow.RecordBatch]
```


[Beta] Create an iterable of class:`pyarrow.RecordBatch`

, to process the table as a stream.

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This method requires the |
`max_queue_size` |
`Optional[int]`
The maximum number of result pages to hold in the internal queue when streaming query results over the BigQuery Storage API. Ignored if Storage API is not used. By default, the max queue size is set to the number of BQ Storage streams created by the server. If |
`max_stream_count` |
`Optional[int]`
The maximum number of parallel download streams when using BigQuery Storage API. Ignored if BigQuery Storage API is not used. This setting also has no effect if the query result is deterministically ordered with ORDER BY, in which case, the number of download stream is always 1. If set to 0 or None (the default), the number of download streams is determined by BigQuery the server. However, this behaviour can require a lot of memory to store temporary download result, especially with very large queries. In that case, setting this parameter value to a value > 0 can help reduce system resource consumption. |

Returns |
|
|---|---|
Type |
Description |
`pyarrow.RecordBatch .. versionadded:: 2.31.0` |
A generator of `pyarrow.RecordBatch` . |

### to_dataframe

```
to_dataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
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


Create a pandas DataFrame by loading all pages of a query.

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This method requires |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`create_bqstorage_client` |
`Optional[bool]`
If |
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
If the `pandas` library cannot be imported, or the bigquery_storage_v1 module is required but cannot be imported. Also if `geography_as_object` is `True` , but the `shapely` library cannot be imported. Also if `bool_dtype` , `int_dtype` or other dtype parameters is not supported dtype. |

Returns |
|
|---|---|
Type |
Description |
`pandas.DataFrame` |
A `pandas.DataFrame` populated with row data and column headers from the query results. The column headers are derived from the destination table's schema. |

### to_dataframe_iterable

```
to_dataframe_iterable(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
max_queue_size: int = object,
max_stream_count: typing.Optional[int] = None,
) -> pandas.DataFrame
```


Create an iterable of pandas DataFrames, to process the table as a stream.

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This method requires |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`max_queue_size` |
`Optional[int]`
The maximum number of result pages to hold in the internal queue when streaming query results over the BigQuery Storage API. Ignored if Storage API is not used. By default, the max queue size is set to the number of BQ Storage streams created by the server. If |
`max_stream_count` |
`Optional[int]`
The maximum number of parallel download streams when using BigQuery Storage API. Ignored if BigQuery Storage API is not used. This setting also has no effect if the query result is deterministically ordered with ORDER BY, in which case, the number of download stream is always 1. If set to 0 or None (the default), the number of download streams is determined by BigQuery the server. However, this behaviour can require a lot of memory to store temporary download result, especially with very large queries. In that case, setting this parameter value to a value > 0 can help reduce system resource consumption. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the `pandas` library cannot be imported. |

Returns |
|
|---|---|
Type |
Description |
`pandas.DataFrame` |
A generator of `pandas.DataFrame` . |

### to_geodataframe

```
to_geodataframe(
bqstorage_client: typing.Optional[bigquery_storage.BigQueryReadClient] = None,
dtypes: typing.Optional[typing.Dict[str, typing.Any]] = None,
progress_bar_type: typing.Optional[str] = None,
create_bqstorage_client: bool = True,
geography_column: typing.Optional[str] = None,
bool_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.BOOL_DTYPE,
int_dtype: typing.Optional[typing.Any] = DefaultPandasDTypes.INT_DTYPE,
float_dtype: typing.Optional[typing.Any] = None,
string_dtype: typing.Optional[typing.Any] = None,
) -> geopandas.GeoDataFrame
```


Create a GeoPandas GeoDataFrame by loading all pages of a query.

Parameters |
|
|---|---|
Name |
Description |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]`
A BigQuery Storage API client. If supplied, use the faster BigQuery Storage API to fetch rows from BigQuery. This method requires the |
`dtypes` |
`Optional[Map[str, Union[str, pandas.Series.dtype]]]`
A dictionary of column names pandas |
`progress_bar_type` |
`Optional[str]`
If set, use the |
`create_bqstorage_client` |
`Optional[bool]`
If |
`geography_column` |
`Optional[str]`
If there are more than one GEOGRAPHY column, identifies which one to use to construct a geopandas GeoDataFrame. This option can be ommitted if there's only one GEOGRAPHY column. |
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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.schema.SerDeInfo -->

# Class SerDeInfo (3.40.0)

```
SerDeInfo(
serialization_library: str,
name: typing.Optional[str] = None,
parameters: typing.Optional[dict[str, str]] = None,
)
```


Serializer and deserializer information.

## Parameters |
|
|---|---|
Name |
Description |
`serialization_library` |
`str`
Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters. |
`name` |
`Optional[str]`
Name of the SerDe. The maximum length is 256 characters. |

## Properties

### name

Optional. Name of the SerDe. The maximum length is 256 characters.

### parameters

Optional. Key-value pairs that define the initialization parameters for the serialization library. Maximum size 10 Kib.

### serialization_library

Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters.

## Methods

### from_api_repr

`from_api_repr(api_repr: dict) -> google.cloud.bigquery.schema.SerDeInfo`


Factory: constructs an instance of the class (cls) given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`api_repr` |
`Dict[str, Any]`
API representation of the object to be instantiated. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel -->

# Class DeterminismLevel (3.40.0)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel -->

# Class DeterminismLevel (3.40.0)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics -->

# Class ArimaFittingMetrics (3.40.0)

`ArimaFittingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ARIMA model fitting metrics.

## Attributes |
|
|---|---|
Name |
Description |
`log_likelihood` |
`float`
Log-likelihood. |
`aic` |
`float`
AIC. |
`variance` |
`float`
Variance. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo -->

# Class SessionInfo (3.40.0)

`SessionInfo(resource)`


[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

## Properties

### session_id

The ID of the session.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/job_base -->

# Common Job Resource Classes

Base classes and helpers for job classes.

*class* google.cloud.bigquery.job.base.ReservationUsage(name, slot_ms)

Job resource usage for a reservation.

Create new instance of ReservationUsage(name, slot_ms)

#### name()

Reservation name or “unreserved” for on-demand resources usage.

#### slot_ms()

Total slot milliseconds used by the reservation for a particular job.

*class* google.cloud.bigquery.job.base.ScriptStackFrame(resource)

Stack frame showing the line/column/procedure name where the current evaluation happened.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* end_column()

One-based end column.

**Type**

*property* end_line()

One-based end line.

**Type**

*property* procedure_id()

Name of the active procedure.

Omitted if in a top-level script.

**Type**Optional[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*property* start_column()

One-based start column.

**Type**

*property* start_line()

One-based start line.

**Type**

*property* text()

Text of the current statement/expression.

**Type**

*class* google.cloud.bigquery.job.base.ScriptStatistics(resource)

Statistics for a child job of a script.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* evaluation_kind(*: Optional[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

Indicates the type of child job.

Possible values include `STATEMENT`

and `EXPRESSION`

.

**Type**

*property* stack_frames(*: Sequence[google.cloud.bigquery.job.base.ScriptStackFrame* )

Stack trace where the current evaluation happened.

Shows line/column/procedure name of each frame on the stack at the point where the current evaluation happened.

The leaf frame is first, the primary script is last.

*class* google.cloud.bigquery.job.base.SessionInfo(resource)

[Preview] Information of the session if this job is part of one.

**Versionadded:** New in version 2.29.0.

**Parameters****resource**(*Map**[**str**, **Any**]*) – JSON representation of object.

*property* session_id(*: Optional[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

The ID of the session.

*class* google.cloud.bigquery.job.base.TransactionInfo(transaction_id: [str](https://docs.python.org/3/library/stdtypes.html#str))

[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

**Versionadded:** New in version 2.24.0.

Create new instance of TransactionInfo(transaction_id,)

#### transaction_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Output only. ID of the transaction.

*class* google.cloud.bigquery.job.base.UnknownJob(job_id, client)

A job whose type cannot be determined.

*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict), client)

Construct an UnknownJob from the JSON representation.

**Parameters****resource**(*Dict*) – JSON representation of a job.**client**() – Client connected to BigQuery API.*google.cloud.bigquery.client.Client*

**Returns**Job corresponding to the resource.

**Return type**UnknownJob

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi -->

# Package dbapi (3.40.0)

API documentation for `bigquery.dbapi`

package.

## Classes

[Connection](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Connection)

DB-API Connection to Google BigQuery.

[Cursor](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor)

DB-API Cursor to Google BigQuery.

[DataError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DataError)

DB-API error due to problems with the processed data.

[DatabaseError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.DatabaseError)

DB-API error related to the database.

[Error](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Error)

Exception representing all non-warning DB-API errors.

[IntegrityError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.IntegrityError)

DB-API error when integrity of the database is affected.

[InterfaceError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InterfaceError)

DB-API error related to the database interface.

[InternalError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InternalError)

DB-API error when the database encounters an internal error.

[NotSupportedError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.NotSupportedError)

DB-API error for operations not supported by the database or API.

[OperationalError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.OperationalError)

DB-API error related to the database operation.

These errors are not necessarily under the control of the programmer.

[ProgrammingError](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.ProgrammingError)

DB-API exception raised for programming errors.

[Warning](/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Warning)

Exception raised for important DB-API warnings.

## Packages Functions

### Binary

`Binary(data)`


Contruct a DB-API binary value.

Parameter |
|
|---|---|
Name |
Description |
`data` |
`bytes-like` An object containing binary data and that can be converted to bytes with the |

### DateFromTicks

`DateFromTicks(timestamp, /)`


Create a date from a POSIX timestamp.

The timestamp is a number, e.g. created via time.time(), that is interpreted as local time.

### TimeFromTicks

`TimeFromTicks(ticks, tz=None)`


Construct a DB-API time value from the given ticks value.

Parameters |
|
|---|---|
Name |
Description |
`ticks` |
`float` a number of seconds since the epoch; see the documentation of the standard Python time module for details. |
`tz` |
`datetime.tzinfo` (Optional) time zone to use for conversion |

### TimestampFromTicks

timestamp[, tz] -> tz's local time from POSIX timestamp.

### connect

`connect(client=None, bqstorage_client=None, prefer_bqstorage_client=True)`


Construct a DB-API connection to Google BigQuery.

Parameters |
|
|---|---|
Name |
Description |
`client` |
`Optional[google.cloud.bigquery.Client]` A REST API client used to connect to BigQuery. If not passed, a client is created using default options inferred from the environment. |
`bqstorage_client` |
`Optional[google.cloud.bigquery_storage_v1.BigQueryReadClient]` A client that uses the faster BigQuery Storage API to fetch rows from BigQuery. If not passed, it is created using the same credentials as |
`prefer_bqstorage_client` |
`Optional[bool]` Prefer the BigQuery Storage client over the REST client. If Storage client isn't available, fall back to the REST client. Defaults to |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest -->

# Python Client for Google BigQuery

Querying massive datasets can be time consuming and expensive without the
right hardware and infrastructure. Google [BigQuery](https://cloud.google.com/bigquery/what-is-bigquery) solves this problem by
enabling super-fast, SQL queries against append-mostly tables, using the
processing power of Google’s infrastructure.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Supported Python Versions

Python >= 3.9

#### Unsupported Python Versions

Python == 2.7, Python == 3.5, Python == 3.6, Python == 3.7, and Python == 3.8.

The last version of this library compatible with Python 2.7 and 3.5 is google-cloud-bigquery==1.28.0.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-bigquery
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-bigquery
```


## Example Usage

### Perform a query

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
# Perform a query.
QUERY = (
'SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` '
'WHERE state = "TX" '
'LIMIT 100')
query_job = client.[query](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)(QUERY) # API request
rows = [query_job](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor.html#google_cloud_bigquery_dbapi_Cursor_query_job).result() # Waits for query to finish
for row in rows:
print(row.name)


## Instrumenting With OpenTelemetry

This application uses [OpenTelemetry](https://opentelemetry.io) to output tracing data from
API calls to BigQuery. To enable OpenTelemetry tracing in
the BigQuery client the following PyPI packages need to be installed:

```
pip install google-cloud-bigquery[opentelemetry] opentelemetry-exporter-gcp-trace
```


After installation, OpenTelemetry can be used in the BigQuery client and in BigQuery jobs. First, however, an exporter must be specified for where the trace data will be outputted to. An example of this can be found here:

```
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.cloud_trace import CloudTraceSpanExporter
tracer_provider = TracerProvider()
tracer_provider = BatchSpanProcessor(CloudTraceSpanExporter())
trace.set_tracer_provider(TracerProvider())
```


In this example all tracing data will be published to the Google
[Cloud Trace](https://cloud.google.com/trace) console. For more information on OpenTelemetry, please consult the [OpenTelemetry documentation](https://opentelemetry-python.readthedocs.io).
