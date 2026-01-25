---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField
fetched_at: 2026-01-25T03:20:36.916331
---

# Class StandardSqlField (3.40.0)


      
      Save and categorize content based on your preferences.

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