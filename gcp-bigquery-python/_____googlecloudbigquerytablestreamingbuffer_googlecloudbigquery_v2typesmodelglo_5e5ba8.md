---
merged_at: 2026-01-26T21:00:49.256263
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigquerytablestreamingbuffer_googlecloudbigquery_v2typesmodelgloba_34faf8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquerytablestreamingbuffer_googlecloudbigquery_v2typesmodelglobal_5a2029.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquerytablestreamingbuffer_googlecloudbigquery_v2typesmodelglobale_9cb763.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerytablestreamingbuffer.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.StreamingBuffer -->

# Class StreamingBuffer (3.40.0)

`StreamingBuffer(resource)`


Information about a table's streaming buffer.

See [https://cloud.google.com/bigquery/streaming-data-into-bigquery](https://cloud.google.com/bigquery/streaming-data-into-bigquery).

## Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
streaming buffer representation returned from the API |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelglobalexplanationexplanation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation.Explanation -->

# Class Explanation (3.40.0)

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`feature_name` |
`str`
Full name of the feature. For non-numerical features, will be formatted like |
`attribution` |
`google.protobuf.wrappers_pb2.DoubleValue`
Attribution of feature. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerystandard_sqlstandardsqlfield.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField -->

# Class StandardSqlField (3.40.0)

```
StandardSqlField(
name: typing.Optional[str] = None,
type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
)
```


A field or a column.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlField)

## Parameters |
|
|---|---|
Name |
Description |
`name` |
`typing.Optional[str]`
The name of this field. Can be absent for struct fields. |
`type` |
`typing.Optional[`
The type of this parameter. Absent if not explicitly specified. For example, CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |

## Properties

### name

The name of this field. Can be absent for struct fields.

### type

The type of this parameter. Absent if not explicitly specified.

For example, CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field).

## Methods

### from_api_repr

`from_api_repr(resource: typing.Dict[str, typing.Any])`


Construct an SQL field instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL field.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumskeyresultstatementkind_googlecloudbigquery_v2typeslist_1cc28c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumskeyresultstatementkind_googlecloudbigquery_v2typeslistm_7f1062.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumskeyresultstatementkind.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.KeyResultStatementKind -->

# Class KeyResultStatementKind (3.40.0)

`KeyResultStatementKind()`


Determines which statement in the script represents the "key result".

The "key result" is used to populate the schema and query results of the script job.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#keyresultstatementkind)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typeslistmodelsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse -->

# Class ListModelsResponse (3.40.0)

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`models` |
`Sequence[`
Models in the requested dataset. Only the following fields are populated: model_reference, model_type, creation_time, last_modified_time and labels. |
`next_page_token` |
`str`
A token to request the next page of results. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobscriptoptions.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.ScriptOptions -->

# Class ScriptOptions (3.40.0)

```
ScriptOptions(
statement_timeout_ms: typing.Optional[int] = None,
statement_byte_budget: typing.Optional[int] = None,
key_result_statement: typing.Optional[
google.cloud.bigquery.enums.KeyResultStatementKind
] = None,
)
```


Options controlling the execution of scripts.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#ScriptOptions)

## Properties

### key_result_statement

Determines which statement in the script represents the "key result".

This is used to populate the schema and query results of the script job.
Default is `KeyResultStatementKind.LAST`

.

### statement_byte_budget

Limit on the number of bytes billed per statement.

Exceeding this budget results in an error.

### statement_timeout_ms

Timeout period for each statement in a script.

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.job.query.ScriptOptions
```


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.ScriptOptions` |
ScriptOptions sample parsed from `resource` . |

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelbinaryclassificationmetricsbinaryconfusionmatr_bbd8ad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelbinaryclassificationmetricsbinaryconfusionmatri_492154.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelbinaryclassificationmetricsbinaryconfusionmatrix.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.BinaryClassificationMetrics.BinaryConfusionMatrix -->

# Class BinaryConfusionMatrix (3.40.0)

`BinaryConfusionMatrix(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Confusion matrix for binary classification models.

## Attributes |
|
|---|---|
Name |
Description |
`positive_class_threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Threshold value used when computing each of the following metric. |
`true_positives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of true samples predicted as true. |
`false_positives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of false samples predicted as true. |
`true_negatives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of true samples predicted as false. |
`false_negatives` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of false samples predicted as false. |
`precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
The fraction of actual positive predictions that had positive actual labels. |
`recall` |
`google.protobuf.wrappers_pb2.DoubleValue`
The fraction of actual positive labels that were given a positive prediction. |
`f1_score` |
`google.protobuf.wrappers_pb2.DoubleValue`
The equally weighted average of recall and precision. |
`accuracy` |
`google.protobuf.wrappers_pb2.DoubleValue`
The fraction of predictions given the correct label. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryscalarqueryparameter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter -->

# Class ScalarQueryParameter (3.40.0)

```
ScalarQueryParameter(
name: typing.Optional[str],
type_: typing.Optional[
typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType]
],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
)
```


Named / positional query parameters for scalar values.

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ScalarQueryParameter`


Factory: construct parameter from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameter` |
Instance |

### positional

```
positional(
type_: typing.Union[str, google.cloud.bigquery.query.ScalarQueryParameterType],
value: typing.Optional[
typing.Union[
str, int, float, decimal.Decimal, bool, datetime.datetime, datetime.date
]
],
) -> google.cloud.bigquery.query.ScalarQueryParameter
```


Factory for positional paramater.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ScalarQueryParameter` |
Instance without name |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapicursor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor -->

# Class Cursor (3.40.0)

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
