---
merged_at: 2026-01-25T12:06:29.146437
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrunjobrequestoverridescontaineroverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.Overrides.ContainerOverride -->

# Class ContainerOverride (0.14.0)

`ContainerOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per-container override specification.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the container specified as a DNS_LABEL. |
`args` |
`MutableSequence[str]`
Optional. Arguments to the entrypoint. Will replace existing args for override. |
`env` |
`MutableSequence[`
List of environment variables to set in the container. Will be merged with existing env for override. |
`clear_args` |
`bool`
Optional. True if the intention is to clear out existing args list. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessourcecode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SourceCode -->

# Class SourceCode (0.14.0)

`SourceCode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source type for the container.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`cloud_storage_source` |
The source is a Cloud Storage bucket. This field is a member of `oneof` _ `source_type` .
|

## Classes

### CloudStorageSource

`CloudStorageSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Cloud Storage source.
