---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query
fetched_at: 2026-01-25T03:16:20.261540
---

# Module query (3.40.0)


      
      Save and categorize content based on your preferences.

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