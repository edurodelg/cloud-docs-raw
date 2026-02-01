---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/dbapi
fetched_at: 2026-02-01T07:59:47.619771
---

# DB-API Reference

Google BigQuery implementation of the Database API Specification v2.0.

This module implements the [Python Database API Specification v2.0 (DB-API)](https://www.python.org/dev/peps/pep-0249/)
for Google BigQuery.

### google.cloud.bigquery.dbapi.Binary(data)

Contruct a DB-API binary value.

**Parameters****data**(*bytes-like*) – An object containing binary data and that can be converted to bytes with the bytes builtin.**Returns**The binary data as a bytes object.

**Return type**

*class* google.cloud.bigquery.dbapi.Connection(client=None, bqstorage_client=None, prefer_bqstorage_client=True)

Bases: `object`


DB-API Connection to Google BigQuery.

**Parameters****client**(*Optional**[**google.cloud.bigquery.Client**]*) – A REST API client used to connect to BigQuery. If not passed, a client is created using default options inferred from the environment.**bqstorage_client**(*Optional**[**google.cloud.bigquery_storage_v1.BigQueryReadClient**]*) – A client that uses the faster BigQuery Storage API to fetch rows from BigQuery. If not passed, it is created using the same credentials as`client`

(provided that BigQuery Storage dependencies are installed).**prefer_bqstorage_client**(*Optional**[**bool**]*) – Prefer the BigQuery Storage client over the REST client. If Storage client isn’t available, fall back to the REST client. Defaults to`True`

.


#### close()

Close the connection and any cursors created from it.

Any BigQuery clients explicitly passed to the constructor are *not*
closed, only those created by the connection instance itself.

#### commit()

No-op, but for consistency raise an error if connection is closed.

#### cursor()

Return a new cursor object.

**Returns**A DB-API cursor that uses this connection.

**Return type**google.cloud.bigquery.dbapi.Cursor


*class* google.cloud.bigquery.dbapi.Cursor(connection)

Bases: `object`


DB-API Cursor to Google BigQuery.

**Parameters****connection**(*google.cloud.bigquery.dbapi.Connection*) – A DB-API connection to Google BigQuery.

#### close()

Mark the cursor as closed, preventing its further use.

#### execute(operation, parameters=None, job_id=None, job_config=None)

Prepare and execute a database operation.

**NOTE**: When setting query parameters, values which are “text”
(`unicode`

in Python2, `str`

in Python3) will use
the ‘STRING’ BigQuery type. Values which are “bytes” (`str`

in
Python2, `bytes`

in Python3), will use using the ‘BYTES’ type.

A ~datetime.datetime parameter without timezone information uses the ‘DATETIME’ BigQuery type (example: Global Pi Day Celebration March 14, 2017 at 1:59pm). A ~datetime.datetime parameter with timezone information uses the ‘TIMESTAMP’ BigQuery type (example: a wedding on April 29, 2011 at 11am, British Summer Time).

For more information about BigQuery data types, see:
[https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types)

`STRUCT`

/`RECORD`

and `REPEATED`

query parameters are not
yet supported. See:
[https://github.com/GoogleCloudPlatform/google-cloud-python/issues/3524](https://github.com/GoogleCloudPlatform/google-cloud-python/issues/3524)

**Parameters****operation**() – A Google BigQuery query string.*str***parameters**(*Union**[**Mapping**[**str**, **Any**]**, **Sequence**[**Any**]**]*) – (Optional) dictionary or sequence of parameter values.**job_id**(* |*str***None*) – (Optional and discouraged) The job ID to use when creating the query job. For best performance and reliability, manually setting a job ID is discouraged.**job_config**() – (Optional) Extra configuration options for the query job.*google.cloud.bigquery.job.QueryJobConfig*


#### executemany(operation, seq_of_parameters)

Prepare and execute a database operation multiple times.

**Parameters**

#### fetchall()

Fetch all remaining results from the last `execute\*()`

call.

**NOTE**: If a dry run query was executed, no rows are returned.

**Returns**A list of all the rows in the results.

**Return type**List[Tuple]

**Raises****google.cloud.bigquery.dbapi.InterfaceError**– if called before`execute()`

.

#### fetchmany(size=None)

Fetch multiple results from the last `execute\*()`

call.

**NOTE**: If a dry run query was executed, no rows are returned.

**NOTE**: The size parameter is not used for the request/response size.
Set the `arraysize`

attribute before calling `execute()`

to
set the batch size.

**Parameters****size**() – (Optional) Maximum number of rows to return. Defaults to the*int*`arraysize`

property value. If`arraysize`

is not set, it defaults to`1`

.**Returns**A list of rows.

**Return type**List[Tuple]

**Raises****google.cloud.bigquery.dbapi.InterfaceError**– if called before`execute()`

.

#### fetchone()

Fetch a single row from the results of the last `execute\*()`

call.

**NOTE**: If a dry run query was executed, no rows are returned.

**Returns**A tuple representing a row or

`None`

if no more data is available.**Return type**Tuple

**Raises****google.cloud.bigquery.dbapi.InterfaceError**– if called before`execute()`

.

*property* query_job(*: Optional[*[google.cloud.bigquery.job.query.QueryJob](/python/docs/reference/bigquery/latest/reference#google.cloud.bigquery.job.QueryJob) )

[google.cloud.bigquery.job.query.QueryJob](/python/docs/reference/bigquery/latest/reference#google.cloud.bigquery.job.QueryJob)

The query job
created by the last `execute\*()`

call, if a query job was created.

**NOTE**: If the last `execute\*()`

call was `executemany()`

, this is the
last job created by `executemany()`

.

**Type**

#### setinputsizes(sizes)

No-op, but for consistency raise an error if cursor is closed.

#### setoutputsize(size, column=None)

No-op, but for consistency raise an error if cursor is closed.

*exception* google.cloud.bigquery.dbapi.DataError()

Bases: `google.cloud.bigquery.dbapi.exceptions.DatabaseError`


DB-API error due to problems with the processed data.

*exception* google.cloud.bigquery.dbapi.DatabaseError()

Bases: `google.cloud.bigquery.dbapi.exceptions.Error`


DB-API error related to the database.

### google.cloud.bigquery.dbapi.Date()

alias of `datetime.date`


### google.cloud.bigquery.dbapi.DateFromTicks(timestamp, /)

Create a date from a POSIX timestamp.

The timestamp is a number, e.g. created via time.time(), that is interpreted as local time.

*exception* google.cloud.bigquery.dbapi.Error()

Bases: `Exception`


Exception representing all non-warning DB-API errors.

*exception* google.cloud.bigquery.dbapi.IntegrityError()

Bases: `google.cloud.bigquery.dbapi.exceptions.DatabaseError`


DB-API error when integrity of the database is affected.

*exception* google.cloud.bigquery.dbapi.InterfaceError()

Bases: `google.cloud.bigquery.dbapi.exceptions.Error`


DB-API error related to the database interface.

*exception* google.cloud.bigquery.dbapi.InternalError()

Bases: `google.cloud.bigquery.dbapi.exceptions.DatabaseError`


DB-API error when the database encounters an internal error.

*exception* google.cloud.bigquery.dbapi.NotSupportedError()

Bases: `google.cloud.bigquery.dbapi.exceptions.DatabaseError`


DB-API error for operations not supported by the database or API.

*exception* google.cloud.bigquery.dbapi.OperationalError()

Bases: `google.cloud.bigquery.dbapi.exceptions.DatabaseError`


DB-API error related to the database operation.

These errors are not necessarily under the control of the programmer.

*exception* google.cloud.bigquery.dbapi.ProgrammingError()

Bases: `google.cloud.bigquery.dbapi.exceptions.DatabaseError`


DB-API exception raised for programming errors.

### google.cloud.bigquery.dbapi.Time()

alias of `datetime.time`


### google.cloud.bigquery.dbapi.TimeFromTicks(ticks, tz=None)

Construct a DB-API time value from the given ticks value.

**Parameters****ticks**() – a number of seconds since the epoch; see the documentation of the standard Python time module for details.*float***tz**() – (Optional) time zone to use for conversion*datetime.tzinfo*

**Returns**time represented by ticks.

**Return type**

### google.cloud.bigquery.dbapi.Timestamp()

alias of `datetime.datetime`


### google.cloud.bigquery.dbapi.TimestampFromTicks()

timestamp[, tz] -> tz’s local time from POSIX timestamp.

*exception* google.cloud.bigquery.dbapi.Warning()

Bases: `Exception`


Exception raised for important DB-API warnings.

### google.cloud.bigquery.dbapi.connect(client=None, bqstorage_client=None, prefer_bqstorage_client=True)

Construct a DB-API connection to Google BigQuery.

**Parameters****client**(*Optional**[**google.cloud.bigquery.Client**]*) – A REST API client used to connect to BigQuery. If not passed, a client is created using default options inferred from the environment.**bqstorage_client**(*Optional**[**google.cloud.bigquery_storage_v1.BigQueryReadClient**]*) – A client that uses the faster BigQuery Storage API to fetch rows from BigQuery. If not passed, it is created using the same credentials as`client`

(provided that BigQuery Storage dependencies are installed).**prefer_bqstorage_client**(*Optional**[**bool**]*) – Prefer the BigQuery Storage client over the REST client. If Storage client isn’t available, fall back to the REST client. Defaults to`True`

.

**Returns**A new DB-API connection to BigQuery.

**Return type**google.cloud.bigquery.dbapi.Connection


# DB-API Query-Parameter Syntax

The BigQuery DB-API uses the qmark [parameter style](https://www.python.org/dev/peps/pep-0249/#paramstyle) for
unnamed/positional parameters and the pyformat parameter style for
named parameters.

An example of a query using unnamed parameters:

```
insert into people (name, income) values (?, ?)
```


and using named parameters:

```
insert into people (name, income) values (%(name)s, %(income)s)
```


## Providing explicit type information

BigQuery requires type information for parameters. The BigQuery DB-API can usually determine parameter types for parameters based on provided values. Sometimes, however, types can’t be determined (for example when None is passed) or are determined incorrectly (for example when passing a floating-point value to a numeric column).

The BigQuery DB-API provides an extended parameter syntax. For named parameters, a BigQuery type is provided after the name separated by a colon, as in:

```
insert into people (name, income) values (%(name:string)s, %(income:numeric)s)
```


For unnamed parameters, use the named syntax with a type, but no name, as in:

```
insert into people (name, income) values (%(:string)s, %(:numeric)s)
```


Providing type information is the *only* way to pass struct data:

```
cursor.execute(
"insert into points (point) values (%(:struct<x float64, y float64>)s)",
[{"x": 10, "y": 20}],
)
```