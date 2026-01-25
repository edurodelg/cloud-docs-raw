---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql
fetched_at: 2026-01-25T03:17:34.437885
---

# Module standard_sql (3.40.0)


      
      Save and categorize content based on your preferences.

API documentation for `bigquery.standard_sql`

module.

## Classes

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlDataType)

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


Parameters |
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

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField)

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

Parameters |
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

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlStructType)

```
StandardSqlStructType(
fields: typing.Optional[
typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField]
] = None,
)
```


Type of a struct field.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType](https://cloud.google.com/bigquery/docs/reference/rest/v2/StandardSqlDataType#StandardSqlStructType)

Parameter |
|
|---|---|
Name |
Description |
`fields` |
`typing.Optional[typing.Iterable[`
The fields in this struct. |

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlTableType)

```
StandardSqlTableType(
columns: typing.Iterable[google.cloud.bigquery.standard_sql.StandardSqlField],
)
```