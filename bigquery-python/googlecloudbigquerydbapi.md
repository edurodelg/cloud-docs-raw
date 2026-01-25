---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi
fetched_at: 2026-01-25T02:05:43.878110
---

# Package dbapi (3.40.0)


      
      Save and categorize content based on your preferences.

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