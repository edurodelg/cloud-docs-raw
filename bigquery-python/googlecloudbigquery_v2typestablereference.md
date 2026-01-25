---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.TableReference
fetched_at: 2026-01-25T03:20:43.507310
---

# Class TableReference (3.40.0)


      
      Save and categorize content based on your preferences.

`TableReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Required. The ID of the project containing this table. |
`dataset_id` |
`str`
Required. The ID of the dataset containing this table. |
`table_id` |
`str`
Required. The ID of the table. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_). The maximum length is 1,024 characters. Certain operations allow suffixing of the table ID with a partition decorator, such as `sample_table$20190123` .
|
`project_id_alternative` |
`Sequence[str]`
The alternative field that will be used when ESF is not able to translate the received data to the project_id field. |
`dataset_id_alternative` |
`Sequence[str]`
The alternative field that will be used when ESF is not able to translate the received data to the project_id field. |
`table_id_alternative` |
`Sequence[str]`
The alternative field that will be used when ESF is not able to translate the received data to the project_id field. |