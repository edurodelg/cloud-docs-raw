---
merged_at: 2026-01-25T15:38:56.570033
merged_files: 2
---

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
