---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType
fetched_at: 2026-01-25T02:14:13.022571
---

# Class StandardSqlDataType (3.40.0)


      
      Save and categorize content based on your preferences.

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