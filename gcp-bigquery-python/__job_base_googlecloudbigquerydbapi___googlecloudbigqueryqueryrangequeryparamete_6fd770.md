---
merged_at: 2026-01-25T15:38:56.571940
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _job_base_googlecloudbigquerydbapi.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: job_base.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/job_base -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerydbapi.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryqueryrangequeryparametertype__googlecloudbigquery_v2typesst_833b81.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryqueryrangequeryparametertype__googlecloudbigquery_v2typessta_b095d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryrangequeryparametertype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType -->

# Class RangeQueryParameterType (3.40.0)

`RangeQueryParameterType(type_, *, name=None, description=None)`


Type representation for range query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`type_` |
`Union[ScalarQueryParameterType, str]`
Type of range element, must be one of 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct parameter type from JSON resource.

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
`google.cloud.bigquery.query.RangeQueryParameterType` |
Instance |

### to_api_repr

`to_api_repr()`


Construct JSON API representation for the parameter type.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |

### with_name

`with_name(new_name: typing.Optional[str])`


Return a copy of the instance with `name`

set to `new_name`

.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Union[str, None]`
The new name of the range query parameter type. If |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameterType` |
A new instance with updated name. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesstandardsqlfield_googlecloudbigquery_v2typesmodellab_fe1c3c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesstandardsqlfield.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField -->

# Class StandardSqlField (3.40.0)

`StandardSqlField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A field or a column.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Optional. The name of this field. Can be absent for struct fields. |
`type` |
Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodellabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LabelsEntry -->

# Class LabelsEntry (3.40.0)

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

## Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesstandardsqldatatype__googlecloudbigquery_v2typesmode_1a8e7e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesstandardsqldatatype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType -->

# Class StandardSqlDataType (3.40.0)

`StandardSqlDataType(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`type_kind` |
Required. The top level type of this field. Can be any standard SQL data type (e.g., "INT64", "DATE", "ARRAY"). |
`array_element_type` |
`google.cloud.bigquery_v2.types.StandardSqlDataType`
The type of the array's elements, if type_kind = "ARRAY". This field is a member of `oneof` _ `sub_type` .
|
`struct_type` |
The fields of this struct, in order, if type_kind = "STRUCT". This field is a member of `oneof` _ `sub_type` .
|

## Classes

### TypeKind

`TypeKind(value)`


API documentation for `bigquery_v2.types.StandardSqlDataType.TypeKind`

class.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelreference_googlecloudbigqueryjobbaseunknownjob.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference -->

# Class ModelReference (3.40.0)

`ModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Id path of a model.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. The ID of the project containing this model. |
`dataset_id` |
`str`
Required. The ID of the dataset containing this model. |
`model_id` |
`str`
Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_). The maximum length is 1,024 characters. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobbaseunknownjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob -->

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
