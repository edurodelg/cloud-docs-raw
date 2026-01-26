---
merged_at: 2026-01-26T21:00:49.251024
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.ExternalRuntimeOptions -->

# Class ExternalRuntimeOptions (3.40.0)

```
ExternalRuntimeOptions(
container_memory: typing.Optional[str] = None,
container_cpu: typing.Optional[int] = None,
runtime_connection: typing.Optional[str] = None,
max_batching_rows: typing.Optional[int] = None,
runtime_version: typing.Optional[str] = None,
_properties: typing.Optional[typing.Dict] = None,
)
```


Options for the runtime of the external system.

## Parameters |
|
|---|---|
Name |
Description |
`container_memory` |
`str`
Optional. Amount of memory provisioned for a Python UDF container instance. Format: {number}{unit} where unit is one of "M", "G", "Mi" and "Gi" (e.g. 1G, 512Mi). If not specified, the default value is 512Mi. For more information, see |
`container_cpu` |
`int`
Optional. Amount of CPU provisioned for a Python UDF container instance. For more information, see |
`runtime_connection` |
`str`
Optional. Fully qualified name of the connection whose service account will be used to execute the code in the container. Format: "projects/{projectId}/locations/{locationId}/connections/{connectionId}" |
`max_batching_rows` |
`int`
Optional. Maximum number of rows in each batch sent to the external runtime. If absent or if 0, BigQuery dynamically decides the number of rows in a batch. |
`runtime_version` |
`str`
Optional. Language runtime version. Example: python-3.11. |

## Properties

### container_cpu

Optional. Amount of CPU provisioned for a Python UDF container instance.

### container_memory

Optional. Amount of memory provisioned for a Python UDF container instance.

### max_batching_rows

Optional. Maximum number of rows in each batch sent to the external runtime.

### runtime_connection

Optional. Fully qualified name of the connection.

### runtime_version

Optional. Language runtime version.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.ExternalRuntimeOptions
```


Factory: construct external runtime options given its API representation.

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
`google.cloud.bigquery.routine.ExternalRuntimeOptions` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this ExternalRuntimeOptions.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
External runtime options represented as an API resource. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob -->

# Class UnknownJob (3.40.0)

`UnknownJob(job_id, client)`


A job whose type cannot be determined.

## Methods

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest -->

# Class PatchModelRequest (3.40.0)

`PatchModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. Project ID of the model to patch. |
`dataset_id` |
`str`
Required. Dataset ID of the model to patch. |
`model_id` |
`str`
Required. Model ID of the model to patch. |
`model` |
Required. Patched model. Follows RFC5789 patch semantics. Missing fields are not updated. To clear a field, explicitly set to default value. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.GoogleSheetsOptions -->

# Class GoogleSheetsOptions (3.40.0)

`GoogleSheetsOptions()`


Options that describe how to treat Google Sheets as BigQuery tables.

## Properties

### range

str: The range of a sheet that BigQuery will query from.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions.FIELDS.range](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#GoogleSheetsOptions.FIELDS.range)

### skip_leading_rows

int: The number of rows at the top of a sheet that BigQuery will skip when reading the data.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.GoogleSheetsOptions
```


Factory: construct a `.external_config.GoogleSheetsOptions`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
`GoogleSheetsOptions` |
Configuration parsed from `resource` . |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.Compression -->

# Class Compression (3.40.0)

`Compression(value)`


The compression type to use for exported files. The default value is
`NONE`

.

`DEFLATE`

and `SNAPPY`

are
only supported for Avro.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DestinationFormat -->

# Class DestinationFormat (3.40.0)

`DestinationFormat()`


The exported file format. The default value is `CSV`

.

Tables with nested or repeated fields cannot be exported as CSV.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType -->

# Class SeasonalPeriodType (3.40.0)

`SeasonalPeriodType(value)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult -->

# Class IterationResult (3.40.0)

`IterationResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single iteration of the training run.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`google.protobuf.wrappers_pb2.Int32Value`
Index of the iteration, 0 based. |
`duration_ms` |
`google.protobuf.wrappers_pb2.Int64Value`
Time taken to run the iteration in milliseconds. |
`training_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the training data at the end of iteration. |
`eval_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Loss computed on the eval data at the end of iteration. |
`learn_rate` |
`float`
Learn rate used for this iteration. |
`cluster_infos` |
`Sequence[`
Information about top clusters for clustering models. |

## Classes

### ArimaResult

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

### ClusterInfo

`ClusterInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Information about a single cluster for clustering model.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.RankingMetrics -->

# Class RankingMetrics (3.40.0)

`RankingMetrics(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation metrics used by weighted-ALS models specified by feedback_type=implicit.

## Attributes |
|
|---|---|
Name |
Description |
`mean_average_precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users. |
`mean_squared_error` |
`google.protobuf.wrappers_pb2.DoubleValue`
Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not. |
`normalized_discounted_cumulative_gain` |
`google.protobuf.wrappers_pb2.DoubleValue`
A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings. |
`average_rank` |
`google.protobuf.wrappers_pb2.DoubleValue`
Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableOptions -->

# Class BigtableOptions (3.40.0)

`BigtableOptions()`


Options that describe how to treat Bigtable tables as BigQuery tables.

## Properties

### column_families

List[`.external_config.BigtableColumnFamily`

]: List of
column families to expose in the table schema along with their types.

### ignore_unspecified_column_families

bool: If :data:`True`

, ignore columns not specified in
`column_families`

list. Defaults to :data:`False`

.

### read_rowkey_as_string

bool: If :data:`True`

, rowkey column families will be read and
converted to string. Defaults to :data:`False`

.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableOptions
```


Factory: construct a `.external_config.BigtableOptions`

instance given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, Any]`
Definition of a |

Returns |
|
|---|---|
Type |
Description |
`BigtableOptions` |
Configuration parsed from `resource` . |

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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/dbapi -->

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
