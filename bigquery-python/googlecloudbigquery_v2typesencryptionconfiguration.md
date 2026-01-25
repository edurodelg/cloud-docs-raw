---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.EncryptionConfiguration
fetched_at: 2026-01-25T03:18:32.088124
---

# Class EncryptionConfiguration (3.40.0)


      
      Save and categorize content based on your preferences.

`EncryptionConfiguration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`kms_key_name` |
`google.protobuf.wrappers_pb2.StringValue`
Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key. |