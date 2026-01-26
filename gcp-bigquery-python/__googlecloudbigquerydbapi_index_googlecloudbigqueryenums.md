---
merged_at: 2026-01-26T21:00:49.242494
merged_files: 2
---


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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums -->

# Module enums (3.40.0)

API documentation for `bigquery.enums`

module.

## Classes

[AutoRowIDs](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.AutoRowIDs)

`AutoRowIDs(value)`


How to handle automatic insert IDs when inserting rows as a stream.

[BigLakeFileFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeFileFormat)

`BigLakeFileFormat()`


API documentation for `bigquery.enums.BigLakeFileFormat`

class.

[BigLakeTableFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.BigLakeTableFormat)

`BigLakeTableFormat()`


API documentation for `bigquery.enums.BigLakeTableFormat`

class.

[Compression](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

[CreateDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.CreateDisposition)

`CreateDisposition()`


Specifies whether the job is allowed to create new tables. The default
value is `CREATE_IF_NEEDED`

.

Creation, truncation and append actions occur as one atomic update upon job completion.

[DatasetView](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DatasetView)

`DatasetView(value)`


DatasetView specifies which dataset information is returned.

[DecimalTargetType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType)

`DecimalTargetType()`


The data types that could be used as a target type when converting decimal values.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType)

.. versionadded:: 2.21.0

[DefaultPandasDTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DefaultPandasDTypes)

`DefaultPandasDTypes(value)`


Default Pandas DataFrem DTypes to convert BigQuery data. These
Sentinel values are used instead of None to maintain backward compatibility,
and allow Pandas package is not available. For more information:
[https://stackoverflow.com/a/60605919/101923](https://stackoverflow.com/a/60605919/101923)

[DestinationFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

[DeterminismLevel](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)

[Encoding](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Encoding)

`Encoding()`


The character encoding of the data. The default is `UTF_8`

.

BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

[EntityTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.EntityTypes)

`EntityTypes(value)`


Enum of allowed entity type names in AccessEntry

[JobCreationMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.JobCreationMode)

`JobCreationMode()`


Documented values for Job Creation Mode.

[KeyResultStatementKind](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.KeyResultStatementKind)

`KeyResultStatementKind()`


Determines which statement in the script represents the "key result".

The "key result" is used to populate the schema and query results of the script job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind)

[QueryApiMethod](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryApiMethod)

`QueryApiMethod(value)`


API method used to start the query. The default value is
`INSERT`

.

[QueryPriority](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.QueryPriority)

`QueryPriority()`


Specifies a priority for the query. The default value is
`INTERACTIVE`

.

[RoundingMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.RoundingMode)

`RoundingMode(value)`


Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

ROUNDING_MODE_UNSPECIFIED: will default to using ROUND_HALF_AWAY_FROM_ZERO.

ROUND_HALF_AWAY_FROM_ZERO: rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5, 1.6, 1.7, 1.8, 1.9 => 2

ROUND_HALF_EVEN: rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5 => 2
- 1.6, 1.7, 1.8, 1.9 => 2
- 2.5 => 2

[SchemaUpdateOption](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SchemaUpdateOption)

`SchemaUpdateOption()`


Specifies an update to the destination table schema as a side effect of a load job.

[SourceColumnMatch](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceColumnMatch)

`SourceColumnMatch(value)`


Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat)

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

[SqlTypeNames](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SqlTypeNames)

`SqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in Legacy SQL.

[StandardSqlTypeNames](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames)

`StandardSqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.

[TimestampPrecision](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.TimestampPrecision)

`TimestampPrecision(value)`


Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

[UpdateMode](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.UpdateMode)

`UpdateMode(value)`


Specifies the kind of information to update in a dataset.

[WriteDisposition](/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.WriteDisposition)

`WriteDisposition()`


Specifies the action that occurs if destination table already exists.

The default value is `WRITE_APPEND`

.

Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.
