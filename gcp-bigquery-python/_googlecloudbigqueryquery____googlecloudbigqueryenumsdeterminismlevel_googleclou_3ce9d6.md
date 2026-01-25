---
merged_at: 2026-01-25T15:38:56.568068
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query -->

# Module query (3.40.0)

BigQuery query processing.

## Classes

[ArrayQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter)

`ArrayQueryParameter(name, array_type, values)`


Named / positional query parameters for array values.

Parameters |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

[ArrayQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameterType)

`ArrayQueryParameterType(array_type, *, name=None, description=None)`


Type representation for array query parameters.

Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[ConnectionProperty](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ConnectionProperty)

`ConnectionProperty(key: str = "", value: str = "")`


A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

Parameters |
|
|---|---|
Name |
Description |
`key` |
`str`
The key of the property to set, for example, |
`value` |
`str`
The value of the property to set. |

[RangeQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter)

`RangeQueryParameter(range_element_type, start=None, end=None, name=None)`


Named / positional query parameters for range values.

Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of 'TIMESTAMP', 'DATE', or 'DATETIME'. |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`name` |
`Optional[str]`
Parameter name, used via |

[RangeQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameterType)

`RangeQueryParameterType(type_, *, name=None, description=None)`


Type representation for range query parameters.

Parameters |
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

[ScalarQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameter)

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

[ScalarQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ScalarQueryParameterType)

`ScalarQueryParameterType(type_, *, name=None, description=None)`


Type representation for scalar query parameters.

Parameters |
|
|---|---|
Name |
Description |
`type_` |
`str`
One of 'STRING', 'INT64', 'FLOAT64', 'NUMERIC', 'BOOL', 'TIMESTAMP', 'DATETIME', or 'DATE'. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[SqlParameterScalarTypes](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.SqlParameterScalarTypes)

`SqlParameterScalarTypes()`


Supported scalar SQL query parameter types as type objects.

[StructQueryParameter](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameter)

`StructQueryParameter(name, *sub_params)`


Name / positional query parameters for struct values.

Parameter |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |

[StructQueryParameterType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType)

`StructQueryParameterType(*fields, name=None, description=None)`


Type representation for struct query parameters.

Parameters |
|
|---|---|
Name |
Description |
`fields` |
`Iterable[Union[ ArrayQueryParameterType, ScalarQueryParameterType, StructQueryParameterType ]]`
An non-empty iterable describing the struct's field types. |
`name` |
`Optional[str]`
The name of the query parameter. Primarily used if the type is one of the subfields in |
`description` |
`Optional[str]`
The query parameter description. Primarily used if the type is one of the subfields in |

[UDFResource](/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.UDFResource)

`UDFResource(udf_type, value)`


Describe a single user-defined function (UDF) resource.

Parameters |
|
|---|---|
Name |
Description |
`udf_type` |
`str`
The type of the resource ('inlineCode' or 'resourceUri') |
`value` |
`str See: https://cloud.google.com/bigquery/user-defined-functions#api`
The inline code or resource URI. |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryenumsdeterminismlevel_googlecloudbigqueryroutinedeterminis_62bf26.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryenumsdeterminismlevel_googlecloudbigqueryroutinedeterminism_854fcb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryenumsdeterminismlevel_googlecloudbigqueryroutinedeterminisml_76c4e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsdeterminismlevel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.DeterminismLevel -->

# Class DeterminismLevel (3.40.0)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutinedeterminismlevel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.DeterminismLevel -->

# Class DeterminismLevel (3.40.0)

`DeterminismLevel()`


Specifies determinism level for JavaScript user-defined functions (UDFs).

[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#DeterminismLevel)


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryquerystructqueryparametertype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.StructQueryParameterType -->

# Class StructQueryParameterType (3.40.0)

`StructQueryParameterType(*fields, name=None, description=None)`


Type representation for struct query parameters.

## Parameters |
|
|---|---|
Name |
Description |
`fields` |
`Iterable[Union[ ArrayQueryParameterType, ScalarQueryParameterType, StructQueryParameterType ]]`
An non-empty iterable describing the struct's field types. |
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
`google.cloud.bigquery.query.StructQueryParameterType` |
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


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelarimafittingmetrics_googlecloudbigqueryjobbase_89bb1a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelarimafittingmetrics_googlecloudbigqueryjobbases_a04594.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelarimafittingmetrics.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaFittingMetrics -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobbasesessioninfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.base.SessionInfo -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobtimelineentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.TimelineEntry -->

# Class TimelineEntry (3.40.0)

`TimelineEntry()`


TimelineEntry represents progress of a query job at a particular point in time.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample](https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#querytimelinesample)
for the underlying API representation within query statistics.

## Properties

### active_units

Optional[int]: Current number of input units being processed by workers, reported as largest value since the last sample.

### completed_units

Optional[int]: Current number of input units completed by this query.

### elapsed_ms

Optional[int]: Milliseconds elapsed since start of query execution.

### pending_units

Optional[int]: Current number of input units remaining for query stages active at this sample time.

### slot_millis

Optional[int]: Cumulative slot-milliseconds consumed by this query.

## Methods

### from_api_repr

`from_api_repr(resource)`


Factory: construct instance from the JSON repr.

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.TimelineEntry` |
Timeline sample parsed from `resource` . |
