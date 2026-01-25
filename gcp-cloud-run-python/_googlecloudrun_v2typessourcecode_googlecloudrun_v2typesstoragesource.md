---
merged_at: 2026-01-25T12:20:14.940604
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesstoragesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.StorageSource -->

# Class StorageSource (0.14.0)

`StorageSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Location of the source in an archive file in Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`bucket` |
`str`
Required. Google Cloud Storage bucket containing the source (see `Bucket Name Requirements |
`object_` |
`str`
Required. Google Cloud Storage object containing the source. This object must be a gzipped archive file ( `.tar.gz` )
containing source to build.
|
`generation` |
`int`
Optional. Google Cloud Storage generation for the object. If the generation is omitted, the latest generation will be used. |
