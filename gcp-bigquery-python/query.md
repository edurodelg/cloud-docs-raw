---
source_url: https://cloud.google.com/python/docs/reference/bigquery/latest/query
fetched_at: 2026-01-25T15:28:54.191901
---

# Query Resource Classes

BigQuery query processing.

*class* google.cloud.bigquery.query.ArrayQueryParameter(name, array_type, values)

Named / positional query parameters for array values.

**Parameters****name**(*Optional**[**str**]*) – Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).**array_type**(*Union**[**str**, **ScalarQueryParameterType**, **StructQueryParameterType**]*) – The type of array elements. If given as a string, it must be one of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BIGNUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATE’, or ‘STRUCT’/’RECORD’. If the type is`'STRUCT'`

/`'RECORD'`

and`values`

is empty, the exact item type cannot be deduced, thus a`StructQueryParameterType`

instance needs to be passed in.**values**(*List**[**appropriate type**]*) – The parameter array values.


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ArrayQueryParameter


*classmethod* positional(array_type: [str](https://docs.python.org/3/library/stdtypes.html#str), values: [list](https://docs.python.org/3/library/stdtypes.html#list))

Factory for positional parameters.

**Parameters****array_type**(*Union**[**str**, **ScalarQueryParameterType**, **StructQueryParameterType**]*) – The type of array elements. If given as a string, it must be one of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BIGNUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATE’, or ‘STRUCT’/’RECORD’. If the type is`'STRUCT'`

/`'RECORD'`

and`values`

is empty, the exact item type cannot be deduced, thus a`StructQueryParameterType`

instance needs to be passed in.**values**(*List**[**appropriate type**]*) – The parameter array values.

**Returns**Instance without name

**Return type**google.cloud.bigquery.query.ArrayQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.ArrayQueryParameterType(array_type, *, name=None, description=None)

Type representation for array query parameters.

**Parameters****array_type**(*Union**[**ScalarQueryParameterType**, **StructQueryParameterType**]*) – The type of array elements.**name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ArrayQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.ConnectionProperty(key: [str](https://docs.python.org/3/library/stdtypes.html#str) = '', value: [str](https://docs.python.org/3/library/stdtypes.html#str) = '')

A connection-level property to customize query behavior.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty](https://cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty)

**Parameters****key**– The key of the property to set, for example,`'time_zone'`

or`'session_id'`

.**value**– The value of the property to set.


*classmethod* from_api_repr(resource)

Construct `ConnectionProperty`

from JSON resource.

**Parameters****resource**– JSON representation.**Returns**A connection property.


*property* key(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Name of the property.

For example:

`time_zone`

`session_id`


#### to_api_repr()

Construct JSON API representation for the connection property.

**Returns**JSON mapping


*property* value(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

Value of the property.

*class* google.cloud.bigquery.query.RangeQueryParameter(range_element_type, start=None, end=None, name=None)

Named / positional query parameters for range values.

**Parameters****range_element_type**(*Union**[**str**, **RangeQueryParameterType**]*) – The type of range elements. It must be one of ‘TIMESTAMP’, ‘DATE’, or ‘DATETIME’.**start**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The start of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.**end**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The end of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.**name**(*Optional**[**str**]*) – Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.RangeQueryParameter


*classmethod* positional(range_element_type, start=None, end=None)

Factory for positional parameters.

**Parameters****range_element_type**(*Union**[**str**, **RangeQueryParameterType**]*) – The type of range elements. It must be one of ‘TIMESTAMP’, ‘DATE’, or ‘DATETIME’.**start**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The start of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.**end**(*Optional**[**Union**[**ScalarQueryParameter**, *[*str*](*][https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**]*) – The end of the range value. Must be the same type as range_element_type. If not provided, it’s interpreted as UNBOUNDED.

**Returns**Instance without name.

**Return type**google.cloud.bigquery.query.RangeQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.RangeQueryParameterType(type_, *, name=None, description=None)

Type representation for range query parameters.

**Parameters****type**(*Union**[**ScalarQueryParameterType**, *[*str*](*]*) – Type of range element, must be one of ‘TIMESTAMP’, ‘DATETIME’, or ‘DATE’.[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str))**name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.RangeQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


#### with_name(new_name: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[str](https://docs.python.org/3/library/stdtypes.html#str)])

Return a copy of the instance with `name`

set to `new_name`

.

**Parameters****name**(*Union**[**str**, **None**]*) – The new name of the range query parameter type. If`None`

, the existing name is cleared.**Returns**A new instance with updated name.

**Return type**google.cloud.bigquery.query.RangeQueryParameterType


*class* google.cloud.bigquery.query.ScalarQueryParameter(name: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[str](https://docs.python.org/3/library/stdtypes.html#str)], type_: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), google.cloud.bigquery.query.ScalarQueryParameterType]], value: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), [int](https://docs.python.org/3/library/functions.html#int), [float](https://docs.python.org/3/library/functions.html#float), [decimal.Decimal](https://docs.python.org/3/library/decimal.html#decimal.Decimal), [bool](https://docs.python.org/3/library/functions.html#bool), [datetime.datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime), [datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date)]])

Named / positional query parameters for scalar values.

**Parameters****name**– Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).**type**– Name of parameter type. Seeand`google.cloud.bigquery.enums.SqlTypeNames`

`google.cloud.bigquery.query.SqlParameterScalarTypes`

for supported types.**value**– The scalar parameter value.


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ScalarQueryParameter


*classmethod* positional(type_: [Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), google.cloud.bigquery.query.ScalarQueryParameterType], value: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[Union](https://docs.python.org/3/library/typing.html#typing.Union)[[str](https://docs.python.org/3/library/stdtypes.html#str), [int](https://docs.python.org/3/library/functions.html#int), [float](https://docs.python.org/3/library/functions.html#float), [decimal.Decimal](https://docs.python.org/3/library/decimal.html#decimal.Decimal), [bool](https://docs.python.org/3/library/functions.html#bool), [datetime.datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime), [datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date)]])

Factory for positional paramater.

**Parameters****type**– Name of parameter type. One of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BIGNUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATETIME’, or ‘DATE’.**value**– The scalar parameter value.

**Returns**Instance without name

**Return type**google.cloud.bigquery.query.ScalarQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.ScalarQueryParameterType(type_, *, name=None, description=None)

Type representation for scalar query parameters.

**Parameters****type**() – One of ‘STRING’, ‘INT64’, ‘FLOAT64’, ‘NUMERIC’, ‘BOOL’, ‘TIMESTAMP’, ‘DATETIME’, or ‘DATE’.*str***name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.ScalarQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


#### with_name(new_name: [Optional](https://docs.python.org/3/library/typing.html#typing.Optional)[[str](https://docs.python.org/3/library/stdtypes.html#str)])

Return a copy of the instance with `name`

set to `new_name`

.

**Parameters****name**(*Union**[**str**, **None**]*) – The new name of the query parameter type. If`None`

, the existing name is cleared.**Returns**A new instance with updated name.

**Return type**google.cloud.bigquery.query.ScalarQueryParameterType


*class* google.cloud.bigquery.query.SqlParameterScalarTypes()

Supported scalar SQL query parameter types as type objects.

*class* google.cloud.bigquery.query.StructQueryParameter(name, *sub_params)

Name / positional query parameters for struct values.

**Parameters****name**(*Optional**[**str**]*) – Parameter name, used via`@foo`

syntax. If None, the parameter can only be addressed via position (`?`

).**(****Union****[****Tuple****[**(*sub_params*) – google.cloud.bigquery.query.ScalarQueryParameter, google.cloud.bigquery.query.ArrayQueryParameter, google.cloud.bigquery.query.StructQueryParameter**]****]****)**– The sub-parameters for the struct


*classmethod* from_api_repr(resource: [dict](https://docs.python.org/3/library/stdtypes.html#dict))

Factory: construct parameter from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.StructQueryParameter


*classmethod* positional(*sub_params)

Factory for positional parameters.

**Parameters****(****Union****[****Tuple****[**(*sub_params*) – google.cloud.bigquery.query.ScalarQueryParameter, google.cloud.bigquery.query.ArrayQueryParameter, google.cloud.bigquery.query.StructQueryParameter**]****]****)**– The sub-parameters for the struct

**Returns**Instance without name

**Return type**google.cloud.bigquery.query.StructQueryParameter


#### to_api_repr()

Construct JSON API representation for the parameter.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.StructQueryParameterType(*fields, name=None, description=None)

Type representation for struct query parameters.

**Parameters****fields**(*Iterable**[**Union**[ **ArrayQueryParameterType**, **ScalarQueryParameterType**, **StructQueryParameterType** ]**]*) – An non-empty iterable describing the struct’s field types.**name**(*Optional**[**str**]*) – The name of the query parameter. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.**description**(*Optional**[**str**]*) – The query parameter description. Primarily used if the type is one of the subfields in`StructQueryParameterType`

instance.


*classmethod* from_api_repr(resource)

Factory: construct parameter type from JSON resource.

**Parameters****resource**(*Dict*) – JSON mapping of parameter**Returns**Instance

**Return type**google.cloud.bigquery.query.StructQueryParameterType


#### to_api_repr()

Construct JSON API representation for the parameter type.

**Returns**JSON mapping

**Return type**Dict


*class* google.cloud.bigquery.query.UDFResource(udf_type, value)

Describe a single user-defined function (UDF) resource.

**Parameters**

See:
[https://cloud.google.com/bigquery/user-defined-functions#api](https://cloud.google.com/bigquery/user-defined-functions#api)