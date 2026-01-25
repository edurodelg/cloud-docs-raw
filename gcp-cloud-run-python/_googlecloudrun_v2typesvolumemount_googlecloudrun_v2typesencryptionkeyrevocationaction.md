---
merged_at: 2026-01-25T12:20:14.949518
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesvolumemount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VolumeMount -->

# Class VolumeMount (0.14.0)

`VolumeMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VolumeMount describes a mounting of a Volume within a container.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. This must match the Name of a Volume. |
`mount_path` |
`str`
Required. Path within the container at which the volume should be mounted. Must not contain ':'. For Cloud SQL volumes, it can be left empty, or must otherwise be `/cloudsql` . All instances defined in the Volume will be
available as `/cloudsql/[instance]` . For more information
on Cloud SQL volumes, visit
https://cloud.google.com/sql/docs/mysql/connect-run
|
`sub_path` |
`str`
Optional. Path within the volume from which the container's volume should be mounted. Defaults to "" (volume's root). |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesencryptionkeyrevocationaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EncryptionKeyRevocationAction -->

# Class EncryptionKeyRevocationAction (0.14.0)

Specifies behavior if an encryption key used by a resource is
revoked.

Enums

Name

Description

ENCRYPTION_KEY_REVOCATION_ACTION_UNSPECIFIED

Unspecified

PREVENT_NEW

Prevents the creation of new instances.

SHUTDOWN

Shuts down existing instances, and prevents creation of new ones.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
