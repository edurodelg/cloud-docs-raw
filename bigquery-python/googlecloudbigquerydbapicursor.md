---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor
fetched_at: 2026-01-25T02:05:48.515746
---

# Class Cursor (3.40.0)


      
      Save and categorize content based on your preferences.

`Cursor(connection)`


DB-API Cursor to Google BigQuery.

## Parameter |
|
|---|---|
Name |
Description |
`connection` |
A DB-API connection to Google BigQuery. |

## Properties

### query_job

[google.cloud.bigquery.job](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job).query.QueryJob | None: The query job
created by the last `execute`

call, if a query job was created.*()*

## Methods

### close

`close()`


Mark the cursor as closed, preventing its further use.

### execute

`execute(operation, parameters=None, job_id=None, job_config=None)`


Prepare and execute a database operation.

A`datetime.datetime`

parameter without timezone information uses
the 'DATETIME' BigQuery type (example: Global Pi Day Celebration
March 14, 2017 at 1:59pm). A `datetime.datetime`

parameter with
timezone information uses the 'TIMESTAMP' BigQuery type (example:
a wedding on April 29, 2011 at 11am, British Summer Time).
```
For more information about BigQuery data types, see:
https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types
`STRUCT`/`RECORD` and `REPEATED` query parameters are not
yet supported. See:
https://github.com/GoogleCloudPlatform/google-cloud-python/issues/3524
```


Parameters |
|
|---|---|
Name |
Description |
`operation` |
`str`
A Google BigQuery query string. |
`parameters` |
`Union[Mapping[str, Any], Sequence[Any]]`
(Optional) dictionary or sequence of parameter values. |
`job_id` |
`str None`
(Optional and discouraged) The job ID to use when creating the query job. For best performance and reliability, manually setting a job ID is discouraged. |
`job_config` |
(Optional) Extra configuration options for the query job. |

### executemany

`executemany(operation, seq_of_parameters)`


Prepare and execute a database operation multiple times.

Parameters |
|
|---|---|
Name |
Description |
`operation` |
`str`
A Google BigQuery query string. |
`seq_of_parameters` |
`Union[Sequence[Mapping[str, Any], Sequence[Any]]]`
Sequence of many sets of parameter values. |

### fetchall

`fetchall()`


Fetch all remaining results from the last `execute*()`

call.

Exceptions |
|
|---|---|
Type |
Description |
|
if called before `execute()` . |

Returns |
|
|---|---|
Type |
Description |
`List[Tuple]` |
A list of all the rows in the results. |

### fetchmany

`fetchmany(size=None)`


Fetch multiple results from the last `execute*()`

call.

Parameter |
|
|---|---|
Name |
Description |
`size` |
`int`
(Optional) Maximum number of rows to return. Defaults to the |

Exceptions |
|
|---|---|
Type |
Description |
|
if called before `execute()` . |

Returns |
|
|---|---|
Type |
Description |
`List[Tuple]` |
A list of rows. |

### fetchone

`fetchone()`


Fetch a single row from the results of the last `execute*()`

call.

Exceptions |
|
|---|---|
Type |
Description |
|
if called before `execute()` . |

Returns |
|
|---|---|
Type |
Description |
`Tuple` |
A tuple representing a row or `None` if no more data is available. |

### setinputsizes

`setinputsizes(sizes)`


No-op, but for consistency raise an error if cursor is closed.

### setoutputsize

`setoutputsize(size, column=None)`


No-op, but for consistency raise an error if cursor is closed.