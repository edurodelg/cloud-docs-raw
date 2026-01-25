---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType
fetched_at: 2026-01-25T03:17:36.651275
---

# Class StandardSqlDataType (3.40.0)


      
      Save and categorize content based on your preferences.

```
StandardSqlDataType(
type_kind: typing.Optional[
google.cloud.bigquery.enums.StandardSqlTypeNames
] = StandardSqlTypeNames.TYPE_KIND_UNSPECIFIED,
array_element_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
struct_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlStructType
] = None,
range_element_type: typing.Optional[
google.cloud.bigquery.standard_sql.StandardSqlDataType
] = None,
)
```


The type of a variable, e.g., a function argument.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType)

Examples:

```
INT64: {type_kind="INT64"}
ARRAY: {type_kind="ARRAY", array_element_type="STRING"}
STRUCT<x STRING, y ARRAY>: {
type_kind="STRUCT",
struct_type={
fields=[
{name="x", type={type_kind="STRING"}},
{
name="y",
type={type_kind="ARRAY", array_element_type="DATE"}
}
]
}
}
RANGE: {type_kind="RANGE", range_element_type="DATETIME"}
```


## Parameters |
|
|---|---|
Name |
Description |
`type_kind` |
`typing.Optional[`
The top level type of this field. Can be any standard SQL data type, e.g. INT64, DATE, ARRAY. |
`array_element_type` |
`typing.Optional[StandardSqlDataType]`
The type of the array's elements, if type_kind is ARRAY. |
`struct_type` |
`typing.Optional[StandardSqlStructType]`
The fields of this struct, in order, if type_kind is STRUCT. |
`range_element_type` |
`typing.Optional[StandardSqlDataType]`
The type of the range's elements, if type_kind is RANGE. |

## Properties

### array_element_type

The type of the array's elements, if type_kind is ARRAY.

### range_element_type

The type of the range's elements, if type_kind = "RANGE". Must be one of DATETIME, DATE, or TIMESTAMP.

### struct_type

The fields of this struct, in order, if type_kind is STRUCT.

### type_kind

The top level type of this field.

Can be any standard SQL data type, e.g. INT64, DATE, ARRAY.

## Methods

### from_api_repr

`from_api_repr(resource: typing.Dict[str, typing.Any])`


Construct an SQL data type instance given its API representation.

### to_api_repr

`to_api_repr() -> typing.Dict[str, typing.Any]`


Construct the API resource representation of this SQL data type.