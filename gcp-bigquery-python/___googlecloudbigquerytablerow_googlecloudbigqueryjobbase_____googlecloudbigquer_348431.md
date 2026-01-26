---
merged_at: 2026-01-26T21:00:49.243563
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.Row -->

# Class Row (3.40.0)

`Row(values, field_to_index)`


A BigQuery row.

Values can be accessed by position (index), by key like a dict, or as properties.

## Parameters |
|
|---|---|
Name |
Description |
`values` |
`Sequence[object]`
The row values |
`field_to_index` |
`Dict[str, int]`
A mapping from schema field names to indexes |

## Methods

### get

`get(key: str, default: typing.Optional[typing.Any] = None) -> typing.Any`


Return a value for key, with a default value if it does not exist.

Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the column to access |
`default` |
`object`
The default value to use if the key does not exist. (Defaults to :data: |

Returns |
|
|---|---|
Type |
Description |
`object .. rubric:: Examples When the key exists, the value associated with it is returned. >>> Row(('a', 'b'), {'x': 0, 'y': 1}).get('x') 'a' The default value is :data:` |
The value associated with the provided key, or a default value. |

### items

`items() -> typing.Iterable[typing.Tuple[str, typing.Any]]`


Return items as `(key, value)`

pairs.

Returns |
|
|---|---|
Type |
Description |
`Iterable[Tuple[str, object]] .. rubric:: Examples >>> list(Row(('a', 'b'), {'x': 0, 'y': 1}).items()) [('x', 'a'), ('y', 'b')]` |
The `(key, value)` pairs representing this row. |

### keys

`keys() -> typing.Iterable[str]`


Return the keys for using a row as a dict.

Returns |
|
|---|---|
Type |
Description |
`Iterable[str] .. rubric:: Examples >>> list(Row(('a', 'b'), {'x': 0, 'y': 1}).keys()) ['x', 'y']` |
The keys corresponding to the columns of a row |

### values

`values()`


Return the values included in this row.

Returns |
|
|---|---|
Type |
Description |
`Sequence[object]` |
A sequence of length `len(row)` . |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base -->

# Module base (3.40.0)

Base classes and helpers for job classes.

## Classes

[ReservationUsage](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ReservationUsage)

`ReservationUsage(name, slot_ms)`


Job resource usage for a reservation.

[ScriptStackFrame](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStackFrame)

`ScriptStackFrame(resource)`


Stack frame showing the line/column/procedure name where the current evaluation happened.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[ScriptStatistics](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.ScriptStatistics)

`ScriptStatistics(resource)`


Statistics for a child job of a script.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[SessionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo)

`SessionInfo(resource)`


[Preview] Information of the session if this job is part of one.

.. versionadded:: 2.29.0

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Map[str, Any]`
JSON representation of object. |

[TransactionInfo](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.TransactionInfo)

`TransactionInfo(transaction_id: str)`


[Alpha] Information of a multi-statement transaction.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#TransactionInfo)

.. versionadded:: 2.24.0

[UnknownJob](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.UnknownJob)

`UnknownJob(job_id, client)`


A job whose type cannot be determined.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.ProgrammingError -->

# Class ProgrammingError (3.40.0)

DB-API exception raised for programming errors.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ModelType -->

# Class ModelType (3.40.0)

`ModelType(value)`


Indicates the type of the Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat -->

# Class ExternalSourceFormat (3.40.0)

`ExternalSourceFormat()`


The format for external data files.

Note that the set of allowed values for external data sources is different
than the set used for loading data (see
[SourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat)).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.IntegrityError -->

# Class IntegrityError (3.40.0)

DB-API error when integrity of the database is affected.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.InternalError -->

# Class InternalError (3.40.0)

DB-API error when the database encounters an internal error.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DecimalTargetType -->

# Class DecimalTargetType (3.40.0)

`DecimalTargetType()`


The data types that could be used as a target type when converting decimal values.

[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#DecimalTargetType)

.. versionadded:: 2.21.0

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.BigtableColumnFamily -->

# Class BigtableColumnFamily (3.40.0)

`BigtableColumnFamily()`


Options for a Bigtable column family.

## Properties

### columns

List[BigtableColumn]: Lists of columns that should be exposed as individual fields.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.columns](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.columns)

### encoding

str: The encoding of the values when the type is not `STRING`


See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.encoding](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.encoding)

### family_id

str: Identifier of the column family.

### only_read_latest

bool: If this is set only the latest version of value are exposed for all columns in this column family.

### type_

str: The type to convert the value in cells of this column family.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#BigtableColumnFamily.FIELDS.type)

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.external_config.BigtableColumnFamily
```


Factory: construct a `.external_config.BigtableColumnFamily`

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
|
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
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineArgument -->

# Class RoutineArgument (3.40.0)

`RoutineArgument(**kwargs)`


Input/output argument of a function or a stored procedure.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#argument)

## Parameter |
|
|---|---|
Name |
Description |
|
`Dict`
Initial property values. |

## Properties

### data_type

Optional[google.cloud.bigquery.StandardSqlDataType]: Type of a variable, e.g., a function argument.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.data_type](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.data_type)

### kind

Optional[str]: The kind of argument, for example `FIXED_TYPE`

or
`ANY_TYPE`

.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.argument_kind](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#Argument.FIELDS.argument_kind)

### mode

Optional[str]: The input/output mode of the argument.

### name

Optional[str]: Name of this argument.

Can be absent for function return argument.

## Methods

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineArgument
```


Factory: construct a routine argument given its API representation.

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
`google.cloud.bigquery.routine.RoutineArgument` |
Python object, as parsed from `resource` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine argument.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine argument represented as an API resource. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Condition -->

# Class Condition (3.40.0)

```
Condition(
expression: str,
title: typing.Optional[str] = None,
description: typing.Optional[str] = None,
)
```


Represents a textual expression in the Common Expression Language (CEL) syntax.

Typically used for filtering or policy rules, such as in IAM Conditions or BigQuery row/column access policies.

See:
[https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr](https://cloud.google.com/iam/docs/reference/rest/Shared.Types/Expr)
[https://github.com/google/cel-spec](https://github.com/google/cel-spec)

## Parameters |
|
|---|---|
Name |
Description |
`expression` |
`str`
The condition expression string using CEL syntax. This is required. Example: |
`title` |
`Optional[str]`
An optional title for the condition, providing a short summary. Example: |
`description` |
`Optional[str]`
An optional description of the condition, providing a detailed explanation. Example: |

## Properties

### description

Optional[str]: The description for the condition.

### expression

str: The expression string for the condition.

### title

Optional[str]: The title for the condition.

## Methods

### __eq__

`__eq__(other: object) -> bool`


Check for equality based on expression, title, and description.

### __hash__

`__hash__() -> int`


Generate a hash based on expression, title, and description.

### __ne__

`__ne__(other: object) -> bool`


Check for inequality.

### __repr__

`__repr__() -> str`


Return a string representation of the Condition object.

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.dataset.Condition
```


Factory: construct a Condition instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this Condition.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.table.SnapshotDefinition -->

# Class SnapshotDefinition (3.40.0)

`SnapshotDefinition(resource: typing.Dict[str, typing.Any])`


Information about base table and snapshot time of the snapshot.

See [https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#snapshotdefinition)

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.SeasonalPeriod -->

# Class SeasonalPeriod (3.40.0)

`SeasonalPeriod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod`

class.

## Classes

### SeasonalPeriodType

`SeasonalPeriodType(value)`


API documentation for `bigquery_v2.types.Model.SeasonalPeriod.SeasonalPeriodType`

class.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SourceFormat -->

# Class SourceFormat (3.40.0)

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.KmeansEnums -->

# Class KmeansEnums (3.40.0)

`KmeansEnums(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `bigquery_v2.types.Model.KmeansEnums`

class.

## Classes

### KmeansInitializationMethod

`KmeansInitializationMethod(value)`


Indicates the method used to initialize the centroids for KMeans clustering algorithm.

---
<!-- Source: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.AggregateClassificationMetrics -->

# Class AggregateClassificationMetrics (3.40.0)

```
AggregateClassificationMetrics(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

## Attributes |
|
|---|---|
Name |
Description |
`precision` |
`google.protobuf.wrappers_pb2.DoubleValue`
Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier. |
`recall` |
`google.protobuf.wrappers_pb2.DoubleValue`
Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric. |
`accuracy` |
`google.protobuf.wrappers_pb2.DoubleValue`
Accuracy is the fraction of predictions given the correct label. For multiclass this is a micro-averaged metric. |
`threshold` |
`google.protobuf.wrappers_pb2.DoubleValue`
Threshold at which the metrics are computed. For binary classification models this is the positive class threshold. For multi-class classfication models this is the confidence threshold. |
`f1_score` |
`google.protobuf.wrappers_pb2.DoubleValue`
The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric. |
`log_loss` |
`google.protobuf.wrappers_pb2.DoubleValue`
Logarithmic Loss. For multiclass this is a macro-averaged metric. |
`roc_auc` |
`google.protobuf.wrappers_pb2.DoubleValue`
Area Under a ROC Curve. For multiclass this is a macro-averaged metric. |
