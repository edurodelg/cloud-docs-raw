---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types
fetched_at: 2026-01-25T03:18:27.397609
---

# Package types (3.40.0)


      
      Save and categorize content based on your preferences.

API documentation for `bigquery_v2.types`

package.

## Classes

[DeleteModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.DeleteModelRequest)

[EncryptionConfiguration](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration)

[GetModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.GetModelRequest)

[ListModelsRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsRequest)

[ListModelsResponse](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ListModelsResponse)

[Model](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model)

[ModelReference](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.ModelReference)

Id path of a model.

[PatchModelRequest](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.PatchModelRequest)

[StandardSqlDataType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlDataType)

The type of a variable, e.g., a function argument. Examples: INT64: {type_kind="INT64"} ARRAY: {type_kind="ARRAY", array_element_type="STRING"} STRUCT<x STRING, y ARRAY>: {type_kind="STRUCT", struct_type={fields=[ {name="x", type={type_kind="STRING"}}, {name="y", type={type_kind="ARRAY", array_element_type="DATE"}} ]}}

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[StandardSqlField](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlField)

A field or a column.

[StandardSqlStructType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType)

[StandardSqlTableType](/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlTableType)

A table type