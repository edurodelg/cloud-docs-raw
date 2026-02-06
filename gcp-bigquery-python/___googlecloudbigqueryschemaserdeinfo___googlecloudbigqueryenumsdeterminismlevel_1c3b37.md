---
merged_at: 2026-02-06T17:08:52.141641
merged_files: 2
---


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
