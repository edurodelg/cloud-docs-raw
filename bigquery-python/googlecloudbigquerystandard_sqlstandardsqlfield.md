---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.standard_sql.StandardSqlField
fetched_at: 2026-01-25T02:11:21.188169
---

# Class StandardSqlField (3.40.0)


      
      Save and categorize content based on your preferences.

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