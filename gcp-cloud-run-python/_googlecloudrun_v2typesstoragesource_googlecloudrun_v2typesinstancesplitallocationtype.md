---
merged_at: 2026-01-25T12:06:29.147368
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesinstancesplitallocationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitAllocationType -->

# Class InstanceSplitAllocationType (0.14.0)

Allocates instances to the Service's latest ready Revision.

INSTANCE_SPLIT_ALLOCATION_TYPE_REVISION

Allocates instances to a Revision by name.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
